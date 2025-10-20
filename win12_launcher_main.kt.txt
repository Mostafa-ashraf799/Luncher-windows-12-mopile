package com.windows12.launcher

import android.app.WallpaperManager
import android.content.Intent
import android.content.pm.ApplicationInfo
import android.content.pm.PackageManager
import android.graphics.Bitmap
import android.graphics.Canvas
import android.graphics.drawable.BitmapDrawable
import android.graphics.drawable.Drawable
import android.os.Bundle
import android.provider.Settings
import android.view.View
import android.widget.GridLayout
import android.widget.ImageButton
import android.widget.ImageView
import android.widget.LinearLayout
import android.widget.ScrollView
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
import androidx.core.content.ContextCompat
import java.text.SimpleDateFormat
import java.util.*

data class AppInfo(
    val name: String,
    val packageName: String,
    val icon: Drawable
)

class MainActivity : AppCompatActivity() {
    
    private lateinit var timeTextView: TextView
    private lateinit var dateTextView: TextView
    private lateinit var appsGrid: GridLayout
    private lateinit var startMenu: LinearLayout
    private lateinit var appsContainer: ScrollView
    private var isStartMenuOpen = false
    private val timeFormat = SimpleDateFormat("HH:mm", Locale.getDefault())
    private val dateFormat = SimpleDateFormat("EEEE, MMMM dd", Locale.getDefault())

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        // تطبيق خلفية Windows 12
        setWindowsBackground()
        
        initializeViews()
        setupStartButton()
        setupQuickSettings()
        updateDateTime()
        loadInstalledApps()
        
        // تحديث الوقت كل دقيقة
        startTimeUpdater()
    }

    private fun setWindowsBackground() {
        val wallpaperManager = WallpaperManager.getInstance(this)
        try {
            // يمكن وضع صورة خلفية Windows 12 هنا
            window.decorView.setBackgroundColor(ContextCompat.getColor(this, R.color.windows_blue))
        } catch (e: Exception) {
            e.printStackTrace()
        }
    }

    private fun initializeViews() {
        timeTextView = findViewById(R.id.timeText)
        dateTextView = findViewById(R.id.dateText)
        appsGrid = findViewById(R.id.appsGrid)
        startMenu = findViewById(R.id.startMenu)
        appsContainer = findViewById(R.id.appsContainer)
    }

    private fun setupStartButton() {
        val startButton = findViewById<ImageButton>(R.id.startButton)
        startButton.setOnClickListener {
            toggleStartMenu()
        }
    }

    private fun setupQuickSettings() {
        findViewById<ImageButton>(R.id.wifiButton).setOnClickListener {
            startActivity(Intent(Settings.ACTION_WIFI_SETTINGS))
        }
        
        findViewById<ImageButton>(R.id.bluetoothButton).setOnClickListener {
            startActivity(Intent(Settings.ACTION_BLUETOOTH_SETTINGS))
        }
        
        findViewById<ImageButton>(R.id.settingsButton).setOnClickListener {
            startActivity(Intent(Settings.ACTION_SETTINGS))
        }
        
        findViewById<ImageButton>(R.id.batteryButton).setOnClickListener {
            startActivity(Intent(Intent.ACTION_POWER_USAGE_SUMMARY))
        }
    }

    private fun toggleStartMenu() {
        isStartMenuOpen = !isStartMenuOpen
        startMenu.visibility = if (isStartMenuOpen) View.VISIBLE else View.GONE
        
        if (isStartMenuOpen) {
            appsContainer.visibility = View.VISIBLE
        }
    }

    private fun updateDateTime() {
        val currentTime = Date()
        timeTextView.text = timeFormat.format(currentTime)
        dateTextView.text = dateFormat.format(currentTime)
    }

    private fun startTimeUpdater() {
        val timer = Timer()
        timer.scheduleAtFixedRate(object : TimerTask() {
            override fun run() {
                runOnUiThread {
                    updateDateTime()
                }
            }
        }, 0, 60000) // تحديث كل دقيقة
    }

    private fun loadInstalledApps() {
        val pm = packageManager
        val apps = pm.getInstalledApplications(PackageManager.GET_META_DATA)
            .filter { (it.flags and ApplicationInfo.FLAG_SYSTEM) == 0 } // التطبيقات غير النظام فقط
            .map { 
                AppInfo(
                    name = it.loadLabel(pm).toString(),
                    packageName = it.packageName,
                    icon = it.loadIcon(pm)
                )
            }
            .sortedBy { it.name }

        displayApps(apps)
    }

    private fun displayApps(apps: List<AppInfo>) {
        appsGrid.removeAllViews()
        appsGrid.columnCount = 4
        
        for (app in apps) {
            val appView = createAppTile(app)
            appsGrid.addView(appView)
        }
    }

    private fun createAppTile(app: AppInfo): View {
        val tileLayout = LinearLayout(this).apply {
            orientation = LinearLayout.VERTICAL
            setPadding(20, 20, 20, 20)
            layoutParams = GridLayout.LayoutParams().apply {
                width = 0
                height = GridLayout.LayoutParams.WRAP_CONTENT
                columnSpec = GridLayout.spec(GridLayout.UNDEFINED, 1f)
                setMargins(10, 10, 10, 10)
            }
            setBackgroundResource(R.drawable.tile_background)
        }

        val iconView = ImageView(this).apply {
            setImageDrawable(app.icon)
            layoutParams = LinearLayout.LayoutParams(120, 120).apply {
                gravity = android.view.Gravity.CENTER
            }
            scaleType = ImageView.ScaleType.FIT_CENTER
        }

        val nameView = TextView(this).apply {
            text = app.name
            textSize = 12f
            setTextColor(ContextCompat.getColor(context, android.R.color.white))
            gravity = android.view.Gravity.CENTER
            maxLines = 2
            setPadding(5, 10, 5, 5)
        }

        tileLayout.addView(iconView)
        tileLayout.addView(nameView)

        tileLayout.setOnClickListener {
            launchApp(app.packageName)
            toggleStartMenu() // إغلاق قائمة Start
        }

        tileLayout.setOnLongClickListener {
            // يمكن إضافة قائمة سياق هنا
            true
        }

        return tileLayout
    }

    private fun launchApp(packageName: String) {
        try {
            val intent = packageManager.getLaunchIntentForPackage(packageName)
            if (intent != null) {
                startActivity(intent)
            }
        } catch (e: Exception) {
            e.printStackTrace()
        }
    }

    override fun onBackPressed() {
        if (isStartMenuOpen) {
            toggleStartMenu()
        } else {
            // لا تفعل شيء للبقاء في الـ launcher
        }
    }

    private fun drawableToBitmap(drawable: Drawable): Bitmap {
        if (drawable is BitmapDrawable) {
            return drawable.bitmap
        }

        val bitmap = Bitmap.createBitmap(
            drawable.intrinsicWidth,
            drawable.intrinsicHeight,
            Bitmap.Config.ARGB_8888
        )
        val canvas = Canvas(bitmap)
        drawable.setBounds(0, 0, canvas.width, canvas.height)
        drawable.draw(canvas)
        return bitmap
    }
}
