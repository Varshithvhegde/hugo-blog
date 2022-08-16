---
title: "Create an Android App with SignUp And SignIn using Firebase"
date: 2022-08-16T21:37:38+05:30
draft: false
cover: 
    image: https://res.cloudinary.com/practicaldev/image/fetch/s--bNhbSODR--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dpbcx2psyistg7ygxq4e.png
    height: 400
    alt: "Website"
    caption: "Simple SignIn SignUp Android App with Firebase"
editPost:
    URL: "https://github.com/Varshithvhegde/hugo-blog/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true
---

### PREREQUISITE:
- Installation of Android Studio. 
- Must be aware of Java language. 
- Basic concepts of android.

## What is firebase?
Firebase is Google's mobile development platform. It provides you the platform to quickly and high-quality app with a better user base. There are multiple complementary features in firebase you can use according to your known needs. 

The main need to connect firebase with the android studio is that the Google repository version is equal to or greater than 26.

## Steps to check the version: 
Click on Tools then on SDK Manager
Click on the SDK tools tab.
Check the Google Repository 
If the Google Repository is not equal to 26 or higher, then install the higher version repository by tapping on install. 
Wait till the installation completes.

## How to connect the project with the firebase?
There are two to connect an app with the firebase:

1. Directly connect your app with the android studio. 
   - Click on the tools and then on firebase.
   - Firebase opens the assistant window.
   - Click on the get started tutorial visible and connect it accordingly.
2. Connect with console.firebase.google.com from home.
    - Open the console firebase.
        
        ![](https://tutorialslink.com/Article_img/Blog_image/4ba15066-2f1e-4167-b747-cf1b57240b88.PNG)
    - Enter the name of the project->continue
        ![](https://tutorialslink.com/Article_img/Blog_image/df8b211a-d45a-45f3-8bb5-736e7e7ab7dc.PNG)
    - Click continue
        ![](https://tutorialslink.com/Article_img/Blog_image/5650223a-1dba-48e5-b4fa-bd0df1181d45.PNG)
        
## What do we do in this android app?

We create a login and registration application and connect both the pages with the firebase for authentication purposes. The information of the user gets register when the user does the registration. Only the registered user can log in other it will show an error message. 

## Components used in the application:

- LinearLayout: It is very easy to work with a linear layout. We can easily set the components to the activity.
- EditText: It is used to take the input from the user. We can also put validations on the text. For example, if we want to take only the number input from the user then we can put the input validations.
- Button: The button needs a user action. It will not work with the user action. It will work only when the user presses a particular button. 
- Toast: Toast is a UI component. It is used to show a short message. We can put the message duration with the help of functions such as LENGTH_LONG AND LENGTH.SHORT. 

## Working of application: 

- For entering into the Home page of the application you need to register. 
- Go to the register page and register yourself. 
- Now move to the login page by entering the email and password from which you have registered. 
- If you have entered the correct details then you will navigate to the home page of the app.  


- XML file of the Registration Page

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    tools:context=".Register">
    <EditText
        android:id="@+id/username"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginRight="4pt"
        android:layout_marginLeft="4pt"
        android:layout_marginTop="10pt"
        android:hint="Username"/>
    <EditText
        android:id="@+id/password1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10pt"
        android:layout_marginLeft="4pt"
        android:layout_marginRight="4pt"
        android:hint="Password"/>
    <Button
        android:id="@+id/sign"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginRight="4pt"
        android:layout_marginLeft="4pt"
        android:layout_marginTop="10pt"
        android:text="SIGN UP"/>


</LinearLayout>

```

- XML file of the Login page

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    tools:context=".login">
    <EditText
        android:id="@+id/email"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginRight="4pt"
        android:layout_marginLeft="4pt"
        android:layout_marginTop="10pt"
        android:hint="Username"/>
    <EditText
        android:id="@+id/password"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10pt"
        android:layout_marginLeft="4pt"
        android:layout_marginRight="4pt"
        android:hint="Password"/>
    <Button
        android:id="@+id/btn_login"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginRight="4pt"
        android:layout_marginLeft="4pt"
        android:layout_marginTop="10pt"
        android:text="LOG IN"/>
    <Button
        android:id="@+id/btn_signup"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginRight="4pt"
        android:layout_marginLeft="4pt"
        android:layout_marginTop="10pt"
        android:text="SIGN UP"/>


</LinearLayout>

```


- Java code of Registration page

```java
package com.example.firebaseaap;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.util.Patterns;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;

public class Register extends AppCompatActivity {
    Button btn2_signup;
    EditText user_name, pass_word;
    FirebaseAuth mAuth;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_register);
        user_name=findViewById(R.id.username);
        pass_word=findViewById(R.id.password1);
        btn2_signup=findViewById(R.id.sign);
        mAuth=FirebaseAuth.getInstance();
        btn2_signup.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String email = user_name.getText().toString().trim();
                String password= pass_word.getText().toString().trim();
                if(email.isEmpty())
                {
                    user_name.setError("Email is empty");
                    user_name.requestFocus();
                    return;
                }
                if(!Patterns.EMAIL_ADDRESS.matcher(email).matches())
                {
                    user_name.setError("Enter the valid email address");
                    user_name.requestFocus();
                    return;
                }
                if(password.isEmpty())
                {
                    pass_word.setError("Enter the password");
                    pass_word.requestFocus();
                    return;
                }
                if(password.length()<6)
                {
                    pass_word.setError("Length of the password should be more than 6");
                    pass_word.requestFocus();
                    return;
                }
                mAuth.createUserWithEmailAndPassword(email,password).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {
                        if(task.isSuccessful())
                        {
                            Toast.makeText(Register.this,"You are successfully Registered", Toast.LENGTH_SHORT).show();
                        }
                        else
                        {
                            Toast.makeText(Register.this,"You are not Registered! Try again",Toast.LENGTH_SHORT).show();
                        }
                    }
                });

            }
        });

    }
}
```

- Java code of Login Page

```java
package com.example.firebaseaap;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.util.Patterns;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import com.google.firebase.auth.FirebaseAuth;

public class login extends AppCompatActivity {
    private EditText user_name, pass_word;
    FirebaseAuth mAuth;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
        user_name=findViewById(R.id.email);
        pass_word=findViewById(R.id.password);
        Button btn_login = findViewById(R.id.btn_login);
        Button btn_sign = findViewById(R.id.btn_signup);
        mAuth=FirebaseAuth.getInstance();
        btn_login.setOnClickListener(v -> {
            String email= user_name.getText().toString().trim();
            String password=pass_word.getText().toString().trim();
            if(email.isEmpty())
            {
                user_name.setError("Email is empty");
                user_name.requestFocus();
                return;
            }
            if(!Patterns.EMAIL_ADDRESS.matcher(email).matches())
            {
                user_name.setError("Enter the valid email");
                user_name.requestFocus();
                return;
            }
            if(password.isEmpty())
            {
                pass_word.setError("Password is empty");
                pass_word.requestFocus();
                return;
            }
            if(password.length()<6)
            {
                pass_word.setError("Length of password is more than 6");
                pass_word.requestFocus();
                return;
            }
            mAuth.signInWithEmailAndPassword(email,password).addOnCompleteListener(task -> {
                if(task.isSuccessful())
                {
                    startActivity(new Intent(login.this, MainActivity.class));
                }
                else
                {
                    Toast.makeText(login.this,
                            "Please Check Your login Credentials",
                            Toast.LENGTH_SHORT).show();
                }

            });
        });
        btn_sign.setOnClickListener(v -> startActivity(new Intent(login.this,Register.class )));
    }

}
```

## Conclusion
Congratulations! You have successfully set up a personal webpage with Hugo and Github Pages.

## Example App
- [Simple SignIn SignUp Source Code](https://github.com/Varshithvhegde/Simple_SignIn_SignUp_Firebase)
