# Notes on DPI and resolution

In windows 10, the pixel size of fonts remains constant irrespective of resolution. That is, the text in the screenshot with a 800x600 resolution takes just as much space in pixels as the same text with a 1920x1080 resolution. There is just much more pixels available in the 1920x1080 resolution. The font sizes in pixels are defined solely by the Windows scaling factor. 

Therefore keeping the monitor size constant, the text with a 1920x1080 resolution appears much smaller for a human than with a 800x600 resolution. The DPI of the physical monitor has drastically changed. 

Confusingly, Windows defines that DPI in both of the above cases is the same, 96. So it's DPI definition is not based on the physical monitor size. The only way that definition makes sense to me, is that the underlying Windows assumption is that the physical screen size is assumed to change proportionally with the resolution and that pixels have a fixed physical width. I guess that might have been true in the early days of computing.

With current monitors \(not even speaking of 4K resolutions\), the resolution certainly doesn't predict the physical size of the monitor. Therefore Windows nowadays offers scaling options. With a scaling of 125% for instance, Windows defines its DPI as 1,25 \* 96 = 120. Let's illustrate this a bit more with an example. 

My 15" laptop has screen dimensions of 34.5cm x 19.5cm \(13.6in x 7.7in\). To match my monitor physical size with the 96 DPI I should be using resolution 1305 x 739 \(nearest standard is 1280 x 720\) and with a 120 DPI \(125% Windows scaling\) I should be using 1632 x 924 resolution \(nearest standard is 1600 x 900\). 

Currently I'm using 1920 x 1080 with a 125% scaling, so Windows says my DPI is 120 although in reality it is 140.

### Links relating to DPI and Windows DPI awareness

* [https://stackoverflow.com/questions/44398075/can-dpi-scaling-be-enabled-disabled-programmatically-on-a-per-session-basis](https://stackoverflow.com/questions/44398075/can-dpi-scaling-be-enabled-disabled-programmatically-on-a-per-session-basis)
* [https://stackoverflow.com/questions/50253948/query-windows-10-8-monitor-scaling-from-python-script](https://stackoverflow.com/questions/50253948/query-windows-10-8-monitor-scaling-from-python-script)
* [https://docs.microsoft.com/en-us/windows/win32/hidpi/high-dpi-desktop-application-development-on-windows?redirectedfrom=MSDN\#common-pitfalls-win32](https://docs.microsoft.com/en-us/windows/win32/hidpi/high-dpi-desktop-application-development-on-windows?redirectedfrom=MSDN#common-pitfalls-win32)
* [https://github.com/rr-/screeninfo](https://github.com/rr-/screeninfo)
* [https://gist.github.com/tlatsas/5311181](https://gist.github.com/tlatsas/5311181)
* [https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/mt846517\(v=vs.85\)](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/mt846517%28v=vs.85%29)

