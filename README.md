MyKidsApp/
├── app/
│   └── src/main/
│       ├── java/com/example/mykidsapp/
│       │   ├── MainActivity.java
│       │   └── AlphabetActivity.java
│       └── res/
│           ├── layout/
│           │   ├── activity_main.xml
│           │   └── activity_alphabet.xml
│           └── raw/
│               ├── a.mp3
│               ├── b.mp3
│               └── c.mp3
├── .gitignore
├── build.gradle (Project)
├── build.gradle (Module: app)
└── settings.gradle

package com.example.mykidsapp;

import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    Button startAlphabetBtn;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        startAlphabetBtn = findViewById(R.id.startAlphabetBtn);
        startAlphabetBtn.setOnClickListener(v -> {
            startActivity(new Intent(MainActivity.this, AlphabetActivity.class));
        });
    }
}

package com.example.mykidsapp;

import android.media.MediaPlayer;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class AlphabetActivity extends AppCompatActivity {
    TextView letterText;
    Button playSoundBtn, nextLetterBtn;
    String[] letters = {"A", "B", "C"};
    int currentIndex = 0;
    MediaPlayer mediaPlayer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_alphabet);
        letterText = findViewById(R.id.letterText);
        playSoundBtn = findViewById(R.id.playSoundBtn);
        nextLetterBtn = findViewById(R.id.nextLetterBtn);
        showLetter();
        playSoundBtn.setOnClickListener(v -> playSound());
        nextLetterBtn.setOnClickListener(v -> {
            currentIndex = (currentIndex + 1) % letters.length;
            showLetter();
        });
    }

    private void showLetter() {
        letterText.setText(letters[currentIndex]);
    }

    private void playSound() {
        if (mediaPlayer != null) mediaPlayer.release();
        int soundId = getResources().getIdentifier(
            letters[currentIndex].toLowerCase(), "raw", getPackageName());
        mediaPlayer = MediaPlayer.create(this, soundId);
        mediaPlayer.start();
    }
}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical"
    android:padding="16dp">

    <Button
        android:id="@+id/startAlphabetBtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Start Alphabet Learning"
        android:textSize="20sp" />
</LinearLayout>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:gravity="center"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/letterText"
        android:text="A"
        android:textSize="100sp"
        android:textColor="#000"
        android:layout_marginTop="50dp" />

    <Button
        android:id="@+id/playSoundBtn"
        android:text="🔊"
        android:textSize="30sp"
        android:layout_marginTop="30dp" />

    <Button
        android:id="@+id/nextLetterBtn"
        android:text="Next"
        android:layout_marginTop="20dp" />
</LinearLayout>
