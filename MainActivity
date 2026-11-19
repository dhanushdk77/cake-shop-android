
package com.dk.cakeshop;

import android.app.Activity;
import android.os.Bundle;
import android.webkit.WebChromeClient;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.view.View;
import android.content.Intent;
import android.net.Uri;
import android.graphics.Color;

public class MainActivity extends Activity {

    private WebView webView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        getWindow().setStatusBarColor(Color.rgb(255,247,245));
        getWindow().setNavigationBarColor(Color.rgb(61,46,49));
        getWindow().getDecorView().setSystemUiVisibility(
            View.SYSTEM_UI_FLAG_LIGHT_STATUS_BAR
        );

        webView = new WebView(this);
        setContentView(webView);

        WebSettings settings = webView.getSettings();
        settings.setJavaScriptEnabled(true);
        settings.setDomStorageEnabled(true);
        settings.setDatabaseEnabled(true);
        settings.setAllowFileAccess(true);
        settings.setAllowContentAccess(true);

        webView.setWebViewClient(new WebViewClient() {

            @Override
            public boolean shouldOverrideUrlLoading(
                WebView view, String url) {

                if (url == null) return false;

                Uri uri = Uri.parse(url);
                String scheme = uri.getScheme();

                if ("https".equalsIgnoreCase(scheme) ||
                    "http".equalsIgnoreCase(scheme) ||
                    "whatsapp".equalsIgnoreCase(scheme)) {

                    if (url.contains("wa.me") ||
                        url.contains("api.whatsapp.com") ||
                        "whatsapp".equalsIgnoreCase(scheme)) {

                        try {
                            Intent intent = new Intent(
                                Intent.ACTION_VIEW, uri
                            );
                            startActivity(intent);
                        } catch (Exception e) {
                            try {
                                Intent browser = new Intent(
                                    Intent.ACTION_VIEW, uri
                                );
                                startActivity(browser);
                            } catch (Exception ignored) {
                            }
                        }

                        return true;
                    }
                }

                return false;
            }
        });

        webView.setWebChromeClient(new WebChromeClient());

        webView.loadUrl("file:///android_asset/index.html");
    }

    @Override
    public void onBackPressed() {
        if (webView != null && webView.canGoBack()) {
            webView.goBack();
        } else {
            super.onBackPressed();
        }
    }
}
