package com.example.order_system;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.NumberPicker;
import android.widget.RadioGroup;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.AdapterView;
import android.widget.CompoundButton;
import android.view.View;
import android.app.Dialog;
import android.widget.Toast;

import java.text.SimpleDateFormat;
import java.util.Calendar;


public class MainActivity extends AppCompatActivity {

    private Button btnOK, btn_mainChange;
    private CheckBox chkShrimp, chkTofu;
    private NumberPicker numPicker;
    private RadioGroup rdgDessert;
    private Spinner sprMain;
    private Dialog mdlg_confirm, mdlg_mainChange;

    private String mainMeal = "", secondMeal = "", dessert = "";
    private int table, mainMoney = 0, secondMoney = 0, total = 0;

    private int count = 0;
    private int sumRevenue = 0;
    //設立空的陣列存放已點餐桌次的資料
    public String[]b;
    public String[]c;
    public String[]d;
    public int[]e;
    //宣告SQLOpenHelper
    private FriendDbOpenHelper mFriendDbOpenHelper;
    //設定今天日期為資料庫名稱
    private static final String DB_FILE =  "'" + new SimpleDateFormat("yyyyMMdd").format(Calendar.getInstance().getTime()) + "'" + ".db", DB_TABLE = "RevenueDetail";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //建立SQLOpenHelper物件
        mFriendDbOpenHelper = new FriendDbOpenHelper(getApplicationContext(),
                DB_FILE, null, 1);
        //取得更改權限
        SQLiteDatabase friendDb = mFriendDbOpenHelper.getWritableDatabase();

        //建立資料表
        Cursor cursor = friendDb.rawQuery("select DISTINCT tbl_name from " +
                "sqlite_master where tbl_name = '" + DB_TABLE + "'", null);
        //建立資料表欄位
        if (cursor != null) {
            if (cursor.getCount() == 0) {
                friendDb.execSQL(" CREATE TABLE '" + DB_TABLE +
                        "'(_id INTEGER PRIMARY KEY," + "tablenumber INTEGER NOT NULL," + "mainMeal TEXT, secondMeal TEXT, dessert TEXT, revenue INTEGER, date DATETIME);");
            }
            //關閉資料表以及cursor
            cursor.close();
        }

        friendDb.close();


        //設定總共10桌的點餐資料初始值
        b = new String[]{"無", "無", "無", "無", "無", "無", "無", "無", "無", "無"};
        c = new String[]{"無", "無", "無", "無", "無", "無", "無", "無", "無", "無"};
        d = new String[]{"無", "無", "無", "無", "無", "無", "無", "無", "無", "無"};
        e = new int[]{0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
        //因為剛開啟時，會沒有check_out回傳的資料，這邊設立try catch 使其不會錯誤無法執行
        try{
            Bundle Main = this.getIntent().getExtras();
            d = Main.getStringArray("sendChkDessert");
            b = Main.getStringArray("sendChkMainMeal");
            c = Main.getStringArray("sendChkSecondMeal");
            e = Main.getIntArray("sendChkTotal");
        }catch (Exception e){
        }

        btnOK = findViewById(R.id.btnOK);
        chkShrimp = findViewById(R.id.chkShrimp);
        chkTofu = findViewById(R.id.chkTofu);
        numPicker = findViewById(R.id.numPicker);
        rdgDessert = findViewById(R.id.rdgDessert);
        sprMain = findViewById(R.id.sprMain);
        //設定版面屬性
        numPicker.setMinValue(1);
        numPicker.setMaxValue(10);
        numPicker.setValue(1);

        sprMain.setOnItemSelectedListener(sprMainOnItemSelected);

        chkShrimp.setOnCheckedChangeListener(chkListener);
        chkTofu.setOnCheckedChangeListener(chkListener);

        btn_mainChange = findViewById(R.id.btn_mainchange);

        btn_mainChange.setOnClickListener(mainChangeOnClick);
        btnOK.setOnClickListener(btnOKClick);

    }

    private AdapterView.OnItemSelectedListener sprMainOnItemSelected = new AdapterView.OnItemSelectedListener() {
        @Override
        public void onItemSelected(AdapterView<?> adapterView, View view, int i, long l) {
            switch (i){
                case 0:
                    mainMeal = getString(R.string.grilledFishSteak);
                    mainMoney = 200;
                    break;
                case 1:
                    mainMeal = getString(R.string.bakedPrawns);
                    mainMoney = 250;
                    break;
                case 2:
                    mainMeal = getString(R.string.frenchRoastChicken);
                    mainMoney = 300;
                    break;
                case 3:
                    mainMeal = getString(R.string.SauteedSteak);
                    mainMoney = 350;
            }
        }

        @Override
        public void onNothingSelected(AdapterView<?> adapterView) {

        }
    };

    private CompoundButton.OnCheckedChangeListener chkListener = new CompoundButton.OnCheckedChangeListener() {
        @Override
        public void onCheckedChanged(CompoundButton compoundButton, boolean b) {

            String secondMealShrimp = "", secondMealTofu = "";
            int moneyShrimp = 0, moneyTofu = 0;

            if(chkShrimp.isChecked()){
                secondMealShrimp = getString(R.string.chkShrimp);
                moneyShrimp = 80;
            }else{
                secondMealShrimp = "";
                moneyShrimp = 0;
            }

            if (chkTofu.isChecked()){
                secondMealTofu = getString(R.string.chkTofu);
                moneyTofu = 50;
            }else{
                secondMealTofu = "";
                moneyTofu = 0;
            }

            secondMeal = secondMealShrimp + "\n" + secondMealTofu;
            secondMoney = moneyShrimp + moneyTofu;
        }
    };

    private View.OnClickListener btnOKClick = new View.OnClickListener() {
        @Override
        public void onClick(View view) {

            table = numPicker.getValue();


            mdlg_confirm = new Dialog(MainActivity.this);
            mdlg_confirm.setCancelable(false);
            mdlg_confirm.requestWindowFeature(android.R.drawable.ic_dialog_info);
            mdlg_confirm.setContentView(R.layout.dlg_confirm);
            mdlg_confirm.setTitle(getString(R.string.dlgTitle));
            mdlg_confirm.show();

            Button dlgBtnOK = mdlg_confirm.findViewById(R.id.dlgbtnOK);
            Button dlgBtnCancel = mdlg_confirm.findViewById(R.id.dlgbtnCancel);
            TextView dlgDessert = mdlg_confirm.findViewById(R.id.dlgDessert);
            TextView dlgMain = mdlg_confirm.findViewById(R.id.dlgMain);
            TextView dlgMoney = mdlg_confirm.findViewById(R.id.dlgMoney);
            TextView dlgSecond = mdlg_confirm.findViewById(R.id.dlgSecond);
            TextView dlgTable = mdlg_confirm.findViewById(R.id.dlgTable);


            switch (rdgDessert.getCheckedRadioButtonId()){
                case R.id.rdbIcecream:
                    dessert = getString(R.string.rdbIceCream);
                    break;
                case R.id.rdbJelly:
                    dessert = getString(R.string.rdbJelly);
            }

            if (secondMeal == "") {
                secondMeal = getString(R.string.nothing);
            }

            total = mainMoney + secondMoney;

            dlgBtnOK.setOnClickListener(DlgBtnOKClick);
            dlgBtnCancel.setOnClickListener(BtnCancelOnClick);
            dlgDessert.setText(dessert);
            dlgMain.setText(mainMeal);
            dlgTable.setText(Integer.toString(table));
            dlgSecond.setText(secondMeal);
            dlgMoney.setText(Integer.toString(total));
        }
    };

    private View.OnClickListener DlgBtnOKClick = new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            mdlg_confirm.dismiss();
            count += 1;
            sumRevenue += total;
            //設定已點餐要先結帳才能在點餐
            if (b[table-1].equals("無")){
                b[table-1] = mainMeal;
                c[table-1] = secondMeal;
                d[table-1] = dessert;
                e[table-1] = total;
                Toast.makeText(getApplicationContext(), getString(R.string.toastOK), Toast.LENGTH_SHORT).show();
            }else{
                mdlg_confirm.dismiss();
                Toast.makeText(getApplicationContext(), getString(R.string.toastFail) + "，" + table + getString(R.string.toastFail2)
                        ,Toast.LENGTH_SHORT).show();
            }

        }
    };

    private View.OnClickListener BtnCancelOnClick = new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            mdlg_confirm.dismiss();
            Toast.makeText(getApplicationContext(), getString(R.string.toastCancel), Toast.LENGTH_SHORT).show();
        }
    };


    private View.OnClickListener mainChangeOnClick = new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            //設定選單屬性
            mdlg_mainChange= new Dialog(MainActivity.this);
            mdlg_mainChange.setCancelable(true);
            mdlg_mainChange.requestWindowFeature(android.R.drawable.ic_dialog_info);
            mdlg_mainChange.setContentView(R.layout.dlg_mainchange);
            mdlg_mainChange.setTitle(getString(R.string.dlgTitle2));
            mdlg_mainChange.show();

            Button returnOrder, dlg_checkout, dlg_form, dlg_end;
            returnOrder = mdlg_mainChange.findViewById(R.id.returnOrder);
            dlg_checkout = mdlg_mainChange.findViewById(R.id.dlg_checkout);
            dlg_form = mdlg_mainChange.findViewById(R.id.dlg_form);
            dlg_end = mdlg_mainChange.findViewById(R.id.dlg_end);

            returnOrder.setOnClickListener(mainItemOnClick);
            dlg_checkout.setOnClickListener(mainItemOnClick);
            dlg_form.setOnClickListener(mainItemOnClick);
            dlg_end.setOnClickListener(mainItemOnClick);

        }

    };

    private View.OnClickListener mainItemOnClick = new View.OnClickListener() {
        @Override
        //設定選單按鈕，可以切換至結帳、表單兩個畫面
        public void onClick(View view) {
            switch (view.getId()){
                case(R.id.returnOrder):
                    mdlg_mainChange.dismiss();
                    break;
                //將點餐資料帶到結帳頁面
                case(R.id.dlg_checkout):                   
                    mdlg_mainChange.dismiss();
                    Intent chk = new Intent();
                    chk.setClass(MainActivity.this, check_out.class);
                    Bundle bundle = new Bundle();
                    bundle.putStringArray("mainMeal", b);
                    bundle.putStringArray("secondMeal", c);
                    bundle.putStringArray("dessert", d);
                    bundle.putIntArray("total", e);
                    chk.putExtras(bundle);
                    startActivity(chk);
                    break;
                case(R.id.dlg_end):
                    mdlg_mainChange.dismiss();
                    finish();
                    break;
                case(R.id.dlg_form):
                    mdlg_mainChange.dismiss();
                    Intent form = new Intent();
                    form.setClass(MainActivity.this, MainActivityForm.class);
                    startActivity(form);
                    break;
            }
        }
    };




}
