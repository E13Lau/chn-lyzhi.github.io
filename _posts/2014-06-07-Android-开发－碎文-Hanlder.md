---
layout: post
title:  "Android-开发－碎文-Hanlder"
date:   2014-06-07 17:45
categories: jekyll update
tags: Android
---


Hanlder 的初步理解：
`Hanlder 作为线程之间通信的信使，可以让线程之间互发信息。`
比如主线程UI线程有一个进度条，我们可以新建一个线程来做某些工作，通过Hanlder返回进度信息进而更新进度条。

简单使用：

```
package com.command.handlertest2.app;

import android.app.Activity;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.ProgressBar;


public class MainActivity extends Activity {

    private Button StartButton;
    private ProgressBar progressBar;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        StartButton = (Button)findViewById(R.id.Start);
        progressBar = (ProgressBar)findViewById(R.id.progressBar);

        StartButton.setOnClickListener(new ProgressBarOnClickListener());

    }

    class ProgressBarOnClickListener implements View.OnClickListener {
        //设置进度条为可见状态
        @Override
        public void onClick(View view) {
            progressBar.setVisibility(view.VISIBLE);
            handler.post(runnable);
        }
    }

    Handler handler = new Handler() {
        @Override
        public void handleMessage(Message msg) {
            progressBar.setProgress(msg.arg1);
            handler.post(runnable);
        }
    };

    Runnable runnable = new Runnable() {
        int i = 0;
        @Override
        public void run() {
            i+=10;
            //得到一个消息对象，Message类是android系统提供的
            Message msg = handler.obtainMessage();
            //将Message对象的arg1参数的值设置为i
            msg.arg1 = i;  //用arg1、arg2这两个成员变量传递消息，优点是系统性能消耗较少
            try {
                Thread.sleep(1000); //让当前线程休眠1000毫秒
            }catch (InterruptedException e) {
                e.printStackTrace();
            }
            //如果i的值等于100
            if (i > 100) {
                //将线程对象从队列中移除
                handler.removeCallbacks(runnable);
                System.out.println("remove Thread");
            }else {
                //将Message对象加入到消息队列当中
                handler.sendMessage(msg);
            }
        }
    };

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();
        if (id == R.id.action_settings) {
            return true;
        }
        return super.onOptionsItemSelected(item);
    }

}
```