
# Ex.No:1 To create a employee details fields and to display the employee details using Firebase Database in Android Studio.


## AIM:

To create and display the employee details using Firebase Database in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display the employee details in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the DatabaseTable using the firebasedatabase”.
Developed by: BARATH V
Registration Number : 212225240023*/
```
## Employee.java
```java
package com.example.employeemanagement;

public class Employee {

    private String id;
    private String name;
    private String age;
    private String salary;

    public Employee() {
    }

    public Employee(String id, String name, String age, String salary) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getAge() {
        return age;
    }

    public String getSalary() {
        return salary;
    }

    public void setId(String id) {
        this.id = id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(String age) {
        this.age = age;
    }

    public void setSalary(String salary) {
        this.salary = salary;
    }
}
```
## MainActivity.java
```java
package com.example.employeemanagement;

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

public class MainActivity extends AppCompatActivity {

    EditText etName, etAge, etSalary;
    Button btnAdd, btnUpdate, btnDelete;

    DatabaseReference databaseReference;

    String currentId = "";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etName = findViewById(R.id.etName);
        etAge = findViewById(R.id.etAge);
        etSalary = findViewById(R.id.etSalary);

        btnAdd = findViewById(R.id.btnAdd);
        btnUpdate = findViewById(R.id.btnUpdate);
        btnDelete = findViewById(R.id.btnDelete);

        databaseReference = FirebaseDatabase.getInstance().getReference("Employees");

        btnAdd.setOnClickListener(v -> {

            String name = etName.getText().toString().trim();
            String age = etAge.getText().toString().trim();
            String salary = etSalary.getText().toString().trim();

            if (name.isEmpty() || age.isEmpty() || salary.isEmpty()) {
                Toast.makeText(MainActivity.this, "Enter all details", Toast.LENGTH_SHORT).show();
                return;
            }

            currentId = databaseReference.push().getKey();

            Employee employee = new Employee(currentId, name, age, salary);

            databaseReference.child(currentId).setValue(employee);

            Toast.makeText(MainActivity.this, "Employee Added Successfully", Toast.LENGTH_SHORT).show();

            etName.setText("");
            etAge.setText("");
            etSalary.setText("");
        });

        btnUpdate.setOnClickListener(v -> {

            if (currentId.isEmpty()) {
                Toast.makeText(MainActivity.this, "Add an employee first", Toast.LENGTH_SHORT).show();
                return;
            }

            Employee employee = new Employee(
                    currentId,
                    etName.getText().toString(),
                    etAge.getText().toString(),
                    etSalary.getText().toString()
            );

            databaseReference.child(currentId).setValue(employee);

            Toast.makeText(MainActivity.this, "Employee Updated", Toast.LENGTH_SHORT).show();
        });

        btnDelete.setOnClickListener(v -> {

            if (currentId.isEmpty()) {
                Toast.makeText(MainActivity.this, "No employee to delete", Toast.LENGTH_SHORT).show();
                return;
            }

            databaseReference.child(currentId).removeValue();

            Toast.makeText(MainActivity.this, "Employee Deleted", Toast.LENGTH_SHORT).show();

            etName.setText("");
            etAge.setText("");
            etSalary.setText("");

            currentId = "";
        });
    }
}
```
## Activity_Main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Employee Name"/>

    <EditText
        android:id="@+id/etAge"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Age"
        android:inputType="number"/>

    <EditText
        android:id="@+id/etSalary"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Salary"
        android:inputType="numberDecimal"/>

    <Button
        android:id="@+id/btnAdd"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="ADD EMPLOYEE"/>

    <Button
        android:id="@+id/btnUpdate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="UPDATE EMPLOYEE"/>

    <Button
        android:id="@+id/btnDelete"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="DELETE EMPLOYEE"/>

</LinearLayout>
```

## OUTPUT:

<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/604644c7-4d1c-4303-a75d-8844be4fc86e" />

<img width="1455" height="445" alt="image" src="https://github.com/user-attachments/assets/ac5cd676-56ac-4cd1-b469-2f4ffa5885a9" />








## RESULT:
Thus a Simple Android Application create a firebase database and to display the employee details using Firbase Real Time Database in Android Studio is developed and executed successfully.
