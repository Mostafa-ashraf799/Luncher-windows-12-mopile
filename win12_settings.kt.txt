package com.windows12.launcher

import android.content.Intent
import android.os.Bundle
import android.provider.Settings
import android.view.View
import android.widget.LinearLayout
import android.widget.TextView
import android.widget.ImageView
import androidx.appcompat.app.AppCompatActivity
import androidx.core.content.ContextCompat

class SettingsActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_settings)

        setupToolbar()
        setupSettingsItems()
    }

    private fun setupToolbar() {
        val backButton = findViewById<ImageView>(R.id.backButton)
        backButton.setOnClickListener {
            finish()
        }

        val titleText = findViewById<TextView>(R.id.toolbarTitle)
        titleText.text = "Settings"
    }

    private fun setupSettingsItems() {
        // System Settings
        findViewById<LinearLayout>(R.id.settingSystem).setOnClickListener {
            startActivity(Intent(Settings.ACTION_SETTINGS))
        }

        // WiFi Settings
        findViewById<LinearLayout>(R.id.settingWifi).setOnClickListener {
            startActivity(Intent(Settings.ACTION_WIFI_SETTINGS))
        }

        // Bluetooth Settings
        findViewById<LinearLayout>(R.id.settingBluetooth).setOnClickListener {
            startActivity(Intent(Settings.ACTION_BLUETOOTH_SETTINGS))
        }

        // Display Settings
        findViewById<LinearLayout>(R.id.settingDisplay).setOnClickListener {
            startActivity(Intent(Settings.ACTION_DISPLAY_SETTINGS))
        }

        // Sound Settings
        findViewById<LinearLayout>(R.id.settingSound).setOnClickListener {
            startActivity(Intent(Settings.ACTION_SOUND_SETTINGS))
        }

        // Storage Settings
        findViewById<LinearLayout>(R.id.settingStorage).setOnClickListener {
            startActivity(Intent(Settings.ACTION_INTERNAL_STORAGE_SETTINGS))
        }

        // Battery Settings
        findViewById<LinearLayout>(R.id.settingBattery).setOnClickListener {
            startActivity(Intent(Intent.ACTION_POWER_USAGE_SUMMARY))
        }

        // Apps Settings
        findViewById<LinearLayout>(R.id.settingApps).setOnClickListener {
            startActivity(Intent(Settings.ACTION_APPLICATION_SETTINGS))
        }

        // Security Settings
        findViewById<LinearLayout>(R.id.settingSecurity).setOnClickListener {
            startActivity(Intent(Settings.ACTION_SECURITY_SETTINGS))
        }

        // About Phone
        findViewById<LinearLayout>(R.id.settingAbout).setOnClickListener {
            startActivity(Intent(Settings.ACTION_DEVICE_INFO_SETTINGS))
        }

        // Launcher Settings
        findViewById<LinearLayout>(R.id.settingLauncher).setOnClickListener {
            openLauncherSettings()
        }
    }

    private fun openLauncherSettings() {
        val intent = Intent(Settings.ACTION_HOME_SETTINGS)
        startActivity(intent)
    }

    override fun onBackPressed() {
        super.onBackPressed()
        finish()
    }
}
