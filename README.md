# Mathematical-Calculator-in-Android-Studio-
To design and develop a mathematical calculator application using Android Studio that performs basic arithmetic operations such as addition, subtraction, multiplication and division through a user-friendly graphical interface.

EXPERIMENT: MATHEMATICAL CALCULATOR USING ANDROID STUDIO
# AIM
To design and develop a mathematical calculator application using Android Studio that performs basic arithmetic operations such as addition, subtraction, multiplication and division through a user-friendly graphical interface.

# SOFTWARE REQUIREMENTS
•	Android Studio
•	Java Programming Language
•	XML Layout Editor
•	Android Emulator or Android Mobile
•	Android SDK

# THEORY
Android Studio is an Integrated Development Environment (IDE) used to develop Android applications. Android applications can be developed using Java and XML.
A mathematical calculator application consists of graphical user interface elements such as:
•	EditText – To enter numerical values.
•	Button – To select arithmetic operations.
•	TextView – To display the calculated result.
Java event-handling methods are used to perform the selected mathematical operations when the user clicks the corresponding buttons.

# PROCEDURE
1.	Open Android Studio.
2.	Select New Project and choose Empty Views Activity.
3.	Enter the project name as MathematicalCalculator.
4.	Select Java as the programming language.
5.	Design the user interface using XML Layout Editor.
6.	Add two EditText fields to enter numerical values.
7.	Add four buttons for Addition, Subtraction, Multiplication and Division.
8.	Add a TextView to display the result.
9.	Open MainActivity.java and write the Java program to perform arithmetic operations.
10.	Use setOnClickListener() to handle button-click events.
11.	Execute the application using an Android Emulator or physical Android device.
12.	Enter two numbers and select the required arithmetic operation.
13.	Verify the displayed result.

# ALGORITHM
1.	Start the application.
2.	Initialize the user interface components.
3.	Accept two numerical inputs from the user.
4.	Select the required arithmetic operation.
5.	Convert the input values into numerical data types.
6.	Perform the selected arithmetic operation.
7.	Check for division by zero when division is selected.
8.	Display the calculated result.
9.	Repeat the process for another operation.
10.	Stop.
# PROGRAM
XML
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/num1"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:autofillHints="number"
        android:hint="@string/hint_num1"
        android:inputType="numberDecimal|numberSigned"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <EditText
        android:id="@+id/num2"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:autofillHints="number"
        android:hint="@string/hint_num2"
        android:inputType="numberDecimal|numberSigned"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/num1" />

    <LinearLayout
        android:id="@+id/buttonLayout"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:orientation="horizontal"
        style="?android:attr/buttonBarStyle"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/num2">

        <Button
            android:id="@+id/btnAdd"
            style="?android:attr/buttonBarButtonStyle"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_marginEnd="4dp"
            android:text="@string/btn_add" />

        <Button
            android:id="@+id/btnSub"
            style="?android:attr/buttonBarButtonStyle"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_marginHorizontal="4dp"
            android:text="@string/btn_sub" />

        <Button
            android:id="@+id/btnMul"
            style="?android:attr/buttonBarButtonStyle"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_marginHorizontal="4dp"
            android:text="@string/btn_mul" />

        <Button
            android:id="@+id/btnDiv"
            style="?android:attr/buttonBarButtonStyle"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_marginStart="4dp"
            android:text="@string/btn_div" />
    </LinearLayout>

    <TextView
        android:id="@+id/result"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:text="@string/result_prefix"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/buttonLayout" />

</androidx.constraintlayout.widget.ConstraintLayout>

KT
package com.example.calculatorapp

import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val n1 = findViewById<EditText>(R.id.num1)
        val n2 = findViewById<EditText>(R.id.num2)
        val result = findViewById<TextView>(R.id.result)

        fun calculate(op: Char) {
            val a = n1.text.toString().toDoubleOrNull()
            val b = n2.text.toString().toDoubleOrNull()
            if ((a == null) || (b == null)) {
                result.text = getString(R.string.error_enter_both)
                return
            }
            val answer = when (op) {
                '+' -> a + b
                '-' -> a - b
                '*' -> a * b
                else -> {
                    if (b == 0.0) {
                        result.text = getString(R.string.error_div_zero)
                        return
                    }
                    a / b
                }
            }
            result.text = getString(R.string.result_format, answer.toString())
        }

        findViewById<Button>(R.id.btnAdd).setOnClickListener { calculate('+') }
        findViewById<Button>(R.id.btnSub).setOnClickListener { calculate('-') }
        findViewById<Button>(R.id.btnMul).setOnClickListener { calculate('*') }
        findViewById<Button>(R.id.btnDiv).setOnClickListener { calculate('/') }
    }
}

```
# KOTLIN PROGRAM
```
kotlin
package com.example.simplecalc   // keep the package name Android Studio generated

import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val n1 = findViewById<EditText>(R.id.num1)
        val n2 = findViewById<EditText>(R.id.num2)
        val result = findViewById<TextView>(R.id.result)

        fun calculate(op: Char) {
            val a = n1.text.toString().toDoubleOrNull()
            val b = n2.text.toString().toDoubleOrNull()
            if (a == null || b == null) {
                result.text = "Enter both numbers"
                return
            }
            val answer = when (op) {
                '+' -> a + b
                '-' -> a - b
                '*' -> a * b
                else -> {
                    if (b == 0.0) { result.text = "Cannot divide by 0"; return }
                    a / b
                }
            }
            result.text = "Result: $answer"
        }

        findViewById<Button>(R.id.btnAdd).setOnClickListener { calculate('+') }
        findViewById<Button>(R.id.btnSub).setOnClickListener { calculate('-') }
        findViewById<Button>(R.id.btnMul).setOnClickListener { calculate('*') }
        findViewById<Button>(R.id.btnDiv).setOnClickListener { calculate('/') }
    }
}
```

# EXPECTED OUTPUT

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/45cfd0e7-adc3-469e-a897-29046e647f0c" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3fc89a04-1711-430c-9d70-d09d01471843" />

# APPLICATION FEATURES
•	Simple and user-friendly interface.
•	Performs four basic arithmetic operations.
•	Accepts numerical inputs from users.
•	Displays calculated results instantly.
•	Handles division-by-zero errors.

# RESULT
Thus, the Mathematical Calculator application was successfully designed and developed using Android Studio with Java and XML. The application performs addition, subtraction, multiplication and division and displays the corresponding results successfully.

# CONCLUSION
The experiment provides practical knowledge of Android application development, XML-based user interface design, Java programming, and event handling using Android Studio.
