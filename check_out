package com.example.order_system;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.widget.AdapterView;
import android.widget.Button;
import android.view.View;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.Toast;

import java.text.SimpleDateFormat;
import java.util.Calendar;

public class check_out extends AppCompatActivity {

    private SQLiteDatabase db;
    Button chkbtnOK;
    TextView chkMain, chkSecond, chkDessert, chkMoney;
    Spinner sprTable;
    private int TableNumber = 0;
    String mydate = java.text.DateFormat.getDateTimeInstance().format(Calendar.getInstance().getTime());

    String[] chkreceivedessert;
    String[] chkreceivemainMeal;
    int[] chkreceivetotal;
    String[] chkreceivesecondMeal;


    int tableNum;


    private final static String CREATE_TABLE = "CREATE TABLE RevenueDetail" +
            "(_id INTEGER PRIMARY KEY, tablenum INTEGER, mainMeal TEXT, secondMeal TEXT, dessert TEXT, revenue INTEGER, date DATETIME)";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_check_out);

        Calendar mCal = Calendar.getInstance();
        String dateformat = "yyyyMMdd";
        SimpleDateFormat df = new SimpleDateFormat(dateformat);
        String today = df.format(mCal.getTime());


        db = openOrCreateDatabase(today + ".db", MODE_PRIVATE, null);

        Bundle bundle = this.getIntent().getExtras();
        chkreceivedessert = bundle.getStringArray("dessert");
        chkreceivemainMeal = bundle.getStringArray("mainMeal");
        chkreceivesecondMeal = bundle.getStringArray("secondMeal");
        chkreceivetotal = bundle.getIntArray("total");

        sprTable = findViewById(R.id.sprTable);
        chkMain = findViewById(R.id.chkMain);
        chkSecond = findViewById(R.id.chkSecond);
        chkDessert = findViewById(R.id.chkDessert);
        chkMoney = findViewById(R.id.chkMoney);

        sprTable.setOnItemSelectedListener(sprTableOnItemSelected);

        chkbtnOK = findViewById(R.id.chkbtnOK);
        chkbtnOK.setOnClickListener(chkbtnOKOnClick);




    }

    private AdapterView.OnItemSelectedListener sprTableOnItemSelected = new AdapterView.OnItemSelectedListener() {
        @Override
        public void onItemSelected(AdapterView<?> adapterView, View view, int i, long l) {

            switch (i){
                case 0:
                    tableNum = 1;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[0]);
                    chkDessert.setText(chkreceivedessert[0]);
                    chkSecond.setText(chkreceivesecondMeal[0]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[0]));
                    break;
                case 1:
                    tableNum = 2;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[1]);
                    chkDessert.setText(chkreceivedessert[1]);
                    chkSecond.setText(chkreceivesecondMeal[1]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[1]));
                    break;
                case 2:
                    tableNum = 3;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[2]);
                    chkDessert.setText(chkreceivedessert[2]);
                    chkSecond.setText(chkreceivesecondMeal[2]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[2]));

                    break;
                case 3:
                    tableNum = 4;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[3]);
                    chkDessert.setText(chkreceivedessert[3]);
                    chkSecond.setText(chkreceivesecondMeal[3]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[3]));

                    break;
                case 4:
                    tableNum = 5;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[4]);
                    chkDessert.setText(chkreceivedessert[4]);
                    chkSecond.setText(chkreceivesecondMeal[4]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[4]));

                    break;
                case 5:
                    tableNum = 6;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[5]);
                    chkDessert.setText(chkreceivedessert[5]);
                    chkSecond.setText(chkreceivesecondMeal[5]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[5]));
                    break;
                case 6:
                    tableNum = 7;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[6]);
                    chkDessert.setText(chkreceivedessert[6]);
                    chkSecond.setText(chkreceivesecondMeal[6]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[6]));
                    break;
                case 7:
                    tableNum = 8;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[7]);
                    chkDessert.setText(chkreceivedessert[7]);
                    chkSecond.setText(chkreceivesecondMeal[7]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[7]));
                    break;
                case 8:
                    tableNum = 9;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[8]);
                    chkDessert.setText(chkreceivedessert[8]);
                    chkSecond.setText(chkreceivesecondMeal[8]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[8]));
                    break;
                case 9:
                    tableNum = 10;
                    chkMain.setText(" ");
                    chkDessert.setText(" ");
                    chkSecond.setText(" ");
                    chkMoney.setText("0");
                    chkMain.setText(chkreceivemainMeal[9]);
                    chkDessert.setText(chkreceivedessert[9]);
                    chkSecond.setText(chkreceivesecondMeal[9]);
                    chkMoney.setText(Integer.toString(chkreceivetotal[9]));

                    break;

            }
        }

        @Override
        public void onNothingSelected(AdapterView<?> adapterView) {

        }
    };

    private View.OnClickListener chkbtnOKOnClick = new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            if (chkMain.getText().equals("無")){
                Toast.makeText(getApplicationContext(), getString(R.string.ToastUnOrder), Toast.LENGTH_SHORT).show();
            }else {

                try {
                    db.execSQL(CREATE_TABLE);
                    db.execSQL("INSERT INTO RevenueDetail (tablenum,mainMeal,secondMeal,dessert,revenue,date) values (" +
                            tableNum + ",'" + chkMain.getText().toString()
                            + "','" + chkSecond.getText() + "','" + chkDessert.getText()
                            + "'," + Integer.parseInt(chkMoney.getText().toString()) + ",'" + mydate + "')");
                } catch (Exception e) {
                }

                chkreceivemainMeal[tableNum - 1] = "無";
                chkreceivetotal[tableNum - 1] = 0;
                chkreceivesecondMeal[tableNum - 1] = "無";
                chkreceivedessert[tableNum - 1] = "無";

                Toast.makeText(check_out.this, getString(R.string.ToastSucess), Toast.LENGTH_SHORT).show();


            }
        }
    };

    @Override
    protected void onPause() {
        super.onPause();
        Intent returnInform = new Intent();
        Bundle chkSendBack = new Bundle();
        returnInform.setClass(check_out.this, MainActivity.class);
        chkSendBack.putStringArray("sendChkMainMeal", chkreceivemainMeal);
        chkSendBack.putStringArray("sendChkSecondMeal", chkreceivesecondMeal);
        chkSendBack.putStringArray("sendChkDessert", chkreceivedessert);
        chkSendBack.putIntArray("sendChkTotal", chkreceivetotal);
        returnInform.putExtras(chkSendBack);
        startActivity(returnInform);
    }

    @Override
    protected void onDestroy(){
        super.onDestroy();
        db.close();
    }

}

