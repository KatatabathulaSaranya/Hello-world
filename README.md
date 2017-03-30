activity_admin_login.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_admin_login"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:background="#6fa8a1"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.AdminLogin">


    <LinearLayout
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:layout_margin="17dp"
            android:inputType="textEmailAddress"
            android:hint="Enter Your Email"
            android:id="@+id/editTextEmail"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <EditText
            android:layout_margin="13dp"
            android:inputType="textPassword"
            android:hint="Password"
            android:id="@+id/editTextPassword"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
        <Button
            android:layout_margin="15dp"
            android:id="@+id/buttonLogin"
            android:text="Login"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />


            />



    </LinearLayout>



</RelativeLayout>

AdminLogin.java

package com.example.nani.firebaseyyp;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;

public class AdminLogin extends AppCompatActivity {

    private Button buttonLogin;
    private EditText editTextEmail;
    private EditText editTextPassword;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_admin_login);
        buttonLogin =(Button) findViewById(R.id.buttonLogin);
        editTextEmail =(EditText) findViewById(R.id.editTextEmail);
        editTextPassword = (EditText) findViewById(R.id.editTextPassword);

    }
}

AndroidMainfest.xml

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.nani.firebaseyyp">

    <user-permission android:name="android.permission.INTERNET" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <!--
 ATTENTION: This was auto-generated to add Google Play services to your project for
     App Indexing.  See https://g.co/AppIndexing/AndroidStudio for more information.
        -->
        <meta-data
            android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

        <activity android:name=".SignActivity" />
        <activity android:name=".AdminLogin" />
        <activity android:name=".products">
            <intent-filter>
                <action android:name="com.example.nani.firebaseyyp.products" />

                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
    </application>

</manifest>
activity_sign.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_sign"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.SignActivity">

</RelativeLayout>

activity_products.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_products"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.products">

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPersonName"
        android:ems="10"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:layout_marginLeft="49dp"
        android:layout_marginStart="49dp"
        android:layout_marginTop="96dp"
        android:id="@+id/pro"
        android:hint="product namr" />

    <Button
        android:text="upload"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/pro"
        android:layout_alignRight="@+id/pro"
        android:layout_alignEnd="@+id/pro"
        android:layout_marginRight="62dp"
        android:layout_marginEnd="62dp"
        android:layout_marginTop="124dp"
        android:id="@+id/ok"
        android:onClick="upload" />
</RelativeLayout>

products.java

package com.example.nani.firebaseyyp;

import android.app.ProgressDialog;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

public class products extends AppCompatActivity {
EditText name;
    Button b;
    private ProgressDialog progressDialog;
    FirebaseDatabase firebaseDatabase;
    DatabaseReference databaseReference;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_products);
        name=(EditText)findViewById(R.id.pro);
        b=(Button)findViewById(R.id.ok);
        progressDialog = new ProgressDialog(this);
        firebaseDatabase=FirebaseDatabase.getInstance();
        databaseReference=firebaseDatabase.getReferenceFromUrl("https://fir-yamyah-project.firebaseio.com/products");
    }


    public void upload(View v)
    {

        DatabaseReference id = databaseReference .push();
        id.child("name").setValue(name.getText().toString());

        Toast.makeText(this, "ok", Toast.LENGTH_SHORT).show();
    }
}

signActivity.java

package com.example.nani.firebaseyyp;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class SignActivity extends AppCompatActivity {


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sign);
    }
}

activity_main.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#6fa8a1"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.MainActivity">



    <LinearLayout
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:layout_margin="17dp"
            android:inputType="textEmailAddress"
            android:hint="Enter Your Email"
            android:id="@+id/editTextEmail"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <EditText
            android:layout_margin="13dp"
            android:inputType="textPassword"
            android:hint="Password"
            android:id="@+id/editTextPassword"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
        <Button
            android:layout_margin="15dp"
            android:id="@+id/buttonRegister"
            android:text="Register User"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <TextView
            android:textAlignment="center"
            android:text="Already Registered? Sign In Here"
            android:id="@+id/textViewSignIn"

            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            />



    </LinearLayout>

    <Button
        android:text="ADMIN Login"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true"
        android:id="@+id/admin" />

    <Button
        android:text="Button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:layout_marginLeft="22dp"
        android:layout_marginStart="22dp"
        android:id="@+id/button2"
        android:onClick="test" />


</RelativeLayout>




