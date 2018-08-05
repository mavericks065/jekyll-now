---
layout: post
title: How to get the result from an Androïd Activity?
---

To start an activity after receiving a result there is in Androïd the method startActivityForResult() ([Java Androïd documentation here](http://developer.android.com/reference/android/app/Activity.html#startActivityForResult(android.content.Intent,%20int)))


What does this method? it launches an Androïd Activity for which you would like a result when the current activity finished her job. Then it calls the onActivityResult() ([doc here](http://developer.android.com/reference/android/app/Activity.html#onActivityResult(int,%20int, android.content.Intent))) of the new activity with an int called the requestCode.

The norm is : if the requestCode is negative calling startActivityForResult() is the same than startActivity(Intent intent)
So the activity that responds must be designed to return a result. This result will be sent as an intent ( Intent : http://developer.android.com/reference/android/content/Intent.html

**ParentActivity.java**
```java
package com.ng.activityresult;

import com.ng.R;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

public class ParentActivity extends Activity {

	private TextView helloWorldViewMessage;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_parent);

		helloWorldViewMessage = (TextView) findViewById(R.id.helloWorldViewMessage);
	}

	// Method to handle the Click Event on GetMessage Button
	public void getMessage(View V) {
		// Create The Intent and Start The Activity to get The message
		Intent intentGetMessage = new Intent(this, ChildActivity.class);
		startActivityForResult(intentGetMessage, 2);
	}

	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		if (requestCode == 2) {
			if (null != data) {
				String message = data.getStringExtra("MESSAGE");
				// Set the message string in textView
				helloWorldViewMessage.setText("Message from child Activity: "
						+ message);
			}
		}
	}

}
```

**ChildActivity.java**
```java
package com.ng.activityresult;

import com.ng.R;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;

public class ChildActivity extends Activity {

	private EditText  editTextMessage;

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_child);
        // Get the reference of Edit Text
        editTextMessage = (EditText) findViewById(R.id.editTextMessage);
    }
    public void submitMessage(View V)
    {
        // get the Entered  message
        String message = editTextMessage.getText().toString();
        Intent intentMessage = new Intent();

        // put the message in Intent
        intentMessage.putExtra("MESSAGE",message);
        setResult(2,intentMessage);
        // finish The activity
        finish();
    }

}

```

Fichiers Layout:

**activity_parent.xml**
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_vertical"
    android:orientation="vertical" >

    <TextView
        android:id="@+id/helloWorldViewMessage"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:gravity="center_horizontal"
        android:textColor="#FF0000"
        android:textSize="20dp"
        android:text="Message" />

    <Button
        android:id="@+id/button1"
        android:layout_marginTop="20dp"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:gravity="center_horizontal"
        android:text="Get Message"
        android:onClick="getMessage" />

</LinearLayout>
```

**activity_child.xml**
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_vertical"
    android:orientation="vertical" >

    <EditText
        android:id="@+id/editTextMessage"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:gravity="center_horizontal"
        android:textColor="#FF0000"
        android:textSize="20sp"
        android:hint="Enter The Message" />

    <Button
        android:layout_marginTop="20dp"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:gravity="center_horizontal"
        android:text="Submit Message"
        android:onClick="submitMessage" />

</LinearLayout>
```





