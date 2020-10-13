# spinnerExam
雙層跟單層

java
----------------------------------------------------------------------------------
package com.sinopac.spinnertest;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    //選幾買幾
    TextView txvShow;
    Spinner spShop, spDrink,classSpinner,divSpinner;
    String selectedClass, selectedDiv;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        txvShow = findViewById(R.id.txvShow);
        spShop = findViewById(R.id.spinnerShop);
        spDrink = findViewById(R.id.spinnerDrink);

        classSpinner = findViewById(R.id.classSpinner);
        divSpinner = findViewById(R.id.divSpinner);


        // Class Spinner implementing onItemSelectedListener
        classSpinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener()
        {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id)
            {
                String selectedClass = parent.getItemAtPosition(position).toString();
                switch (selectedClass)
                {
                    case "Class 1":
                        // assigning div item list defined in XML to the div Spinner
                        divSpinner.setAdapter(new ArrayAdapter<String>(MainActivity.this,
                                android.R.layout.simple_spinner_dropdown_item,
                                getResources().getStringArray(R.array.items_div_class_1)));
                        break;

                    case "Class 2":
                        divSpinner.setAdapter(new ArrayAdapter<String>(MainActivity.this,
                                android.R.layout.simple_spinner_dropdown_item,
                                getResources().getStringArray(R.array.items_div_class_2)));
                        break;

                    case "Class 3":
                        divSpinner.setAdapter(new ArrayAdapter<String>(MainActivity.this,
                                android.R.layout.simple_spinner_dropdown_item,
                                getResources().getStringArray(R.array.items_div_class_3)));
                        break;

                    case "Class 4":
                        divSpinner.setAdapter(new ArrayAdapter<String>(MainActivity.this,
                                android.R.layout.simple_spinner_dropdown_item,
                                getResources().getStringArray(R.array.items_div_class_4)));
                        break;
                }

                //set divSpinner Visibility to Visible
                divSpinner.setVisibility(View.VISIBLE);
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent)
            {
                // can leave this empty
            }
        });

        // Div Spinner implementing onItemSelectedListener
        divSpinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener()
        {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id)
            {
                selectedDiv = parent.getItemAtPosition(position).toString();
                /*
                    Now that we have both values, lets create a Toast to
                    show the values on screen
                */
                Toast.makeText(MainActivity.this, "\n Class: \t " + selectedClass +
                        "\n Div: \t" + selectedDiv, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent)
            {
                // can leave this empty
            }

        });
    }



    //選幾買幾 範例
    public void buy (View view){
        //指定字串陣列，對應到資源檔的字串陣列
        String[] shop =getResources().getStringArray(R.array.shop);
        String[] drink = getResources().getStringArray(R.array.drinks);

        //取得被選擇的項目編號(各個選單有各自的編號)
        int idShop=spShop.getSelectedItemPosition();
        int idDrink=spDrink.getSelectedItemPosition();

        //shop就是剛剛的字串陣列，[]中為指定的項目，組合為讀取對應字串陣列對應位置的內容
        txvShow.setText("買"+shop[idShop]+"的"+drink[idDrink]);

    }
}
----------------------------------------------------------------------------------------
XML
----------------------------------------------------------------------------------------
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:orientation="vertical">

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <TextView
                android:id="@+id/textView2"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="飲料店:"
                android:textSize="24sp" />

            <Spinner
                android:id="@+id/spinnerShop"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginStart="24dp"
                android:entries="@array/shop" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <TextView
                android:id="@+id/textView"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="飲料:"
                android:textSize="24sp" />

            <Spinner
                android:id="@+id/spinnerDrink"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:entries="@array/drinks" />
        </LinearLayout>

        <Button
            android:id="@+id/btnBuy"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="buy"
            android:text="買"
            android:textSize="30sp" />

        <TextView
            android:id="@+id/txvShow"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginBottom="276dp"
            android:textSize="30sp" />

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:orientation="vertical">


        <Spinner
            android:id="@+id/classSpinner"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@+id/tvDemo"
            android:layout_marginTop="25dp"
            android:entries="@array/items_class"/>

        <Spinner
            android:id="@+id/divSpinner"
            android:visibility="gone"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/classSpinner"
            android:layout_toLeftOf="@id/classSpinner"
            android:layout_marginTop="10dp"
            />

    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
-----------------------------------------------------------------------------
strings
---------------------------------------------------------------------------
<resources>
    <string name="app_name">spinnertest</string>
    <string-array name="shop">
        <item>1</item>
        <item>2</item>
        <item>3</item>
        <item>4</item>
        <item>5</item>
        <item>6</item>
    </string-array>

    <string-array name="drinks">
        <item>選項1</item>
        <item>選項2</item>
        <item>選項3</item>
        <item>選項4</item>
        <item>選項5</item>
    </string-array>


    <string-array name="items_class">
        <item>Class 1</item>
        <item>Class 2</item>
        <item>Class 3</item>
        <item>Class 4</item>
    </string-array>

    <string-array name="items_div_class_1">
        <item>Div 1-A</item>
        <item>Div 1-B</item>
        <item>Div 1-C</item>
        <item>Div 1-D</item>
    </string-array>

    <string-array name="items_div_class_2">
        <item>Div 2-A</item>
        <item>Div 2-B</item>
        <item>Div 2-C</item>
        <item>Div 2-D</item>
    </string-array>

    <string-array name="items_div_class_3">
        <item>Div 3-A</item>
        <item>Div 3-B</item>
        <item>Div 3-C</item>
        <item>Div 3-D</item>
    </string-array>

    <string-array name="items_div_class_4">
        <item>Div 4-A</item>
        <item>Div 4-B</item>
        <item>Div 4-C</item>
        <item>Div 4-D</item>
    </string-array>
</resources>


