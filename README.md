
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```

Program to print the text create your own content providers to get contacts details.
Developed by: SATHANA V
Register Number: 212224220091

```

## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:text="Contact Details"
        android:textSize="25sp"
        android:textStyle="bold" />

    <Button
        android:id="@+id/btnContacts"
        android:layout_width="match_parent"
        android:layout_height="91dp"
        android:text="Display Contacts" />

    <TextView
        android:id="@+id/txtContacts"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="18sp"
        android:padding="10dp"/>

</LinearLayout>
```

## MainActivity.java
```
package com.example.contact;

import android.Manifest;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity {

    Button btnContacts;
    TextView txtContacts;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnContacts = findViewById(R.id.btnContacts);
        txtContacts = findViewById(R.id.txtContacts);

        btnContacts.setOnClickListener(v -> {

            if (ContextCompat.checkSelfPermission(this,
                    Manifest.permission.READ_CONTACTS)
                    != PackageManager.PERMISSION_GRANTED) {

                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.READ_CONTACTS}, 1);

            } else {
                displayContacts();
            }
        });
    }

    private void displayContacts() {

        StringBuilder contacts = new StringBuilder();

        Cursor cursor = getContentResolver().query(
                ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
                null, null, null, null);

        if (cursor != null) {

            while (cursor.moveToNext()) {

                String name = cursor.getString(
                        cursor.getColumnIndexOrThrow(
                                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));

                String number = cursor.getString(
                        cursor.getColumnIndexOrThrow(
                                ContactsContract.CommonDataKinds.Phone.NUMBER));

                contacts.append("Name: ").append(name)
                        .append("\nPhone: ").append(number)
                        .append("\n\n");
            }

            cursor.close();
        }

        txtContacts.setText(contacts.length() == 0
                ? "No contacts found"
                : contacts.toString());
    }

    @Override
    public void onRequestPermissionsResult(int requestCode,
                                           String[] permissions, int[] grantResults) {

        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        if (requestCode == 1 && grantResults.length > 0
                && grantResults[0] == PackageManager.PERMISSION_GRANTED) {

            displayContacts();

        } else {
            Toast.makeText(this, "Permission Denied",
                    Toast.LENGTH_SHORT).show();
        }
    }
}
```
## AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.contact"
    xmlns:tools="http://schemas.android.com/tools">
    <uses-permission android:name="android.permission.READ_CONTACTS"/>
    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Contact">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:windowSoftInputMode="adjustResize">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

## OUTPUT

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/c19c124b-ba7b-41f2-9918-3e6128c6955a" />
<img width="1920" height="1200" alt="Screenshot (145)" src="https://github.com/user-attachments/assets/b1acc620-7048-419f-91b8-6acef6bae685" />



## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
