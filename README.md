# Kurdish Keyboard کیبۆردی کوردی
<div dir=rtl>

### **١. پێشەکی**

کارکردنی ئێمە لەسەر Android Studioییە.

### **٢. دروستکردنی پڕۆژەیەکی نوێ**

سەرەتا، پڕۆژەیەکی نوێ دروست دەکەین و ناوی دەنێین (Keyboard\_KU\_EN)، هەنگاوەکانی تر بە دروست و گونجاوی تێپەڕێنن، ئێمە بۆ بابەتی ئەم جارە نەخشەی Empty Activity هەڵدەبژێرین، وە ناوی Activityیەکە دەنێین (keyboard_androkurd) وە ناوی Layoutش دەنێین (keyboard). ![keyboard](https://user-images.githubusercontent.com/42367292/44075360-37bfa9c6-9fa5-11e8-84a3-f96da70d95b1.jpg) چاوێک لەم بابەتە بکە بۆ زانیاری زۆرتر لەسەر دروستکردنی پڕۆژەیەک لە ئەندرۆید ستۆدیۆ **[کرتە بکە](http://androkurd.com/arshif/3701)**.

### **٣. دەسکاریکردنی Manifest**

هەر تەختەکلیلێک بۆ ناسینەوەی لە سیستەمی ئەندرۆیدا (Input Method Editor (IMEێک وەردەگرێت, هەر IMEێک سوود لە پێکهاتەی Service وەردەگرێت بۆ ناسینەوەی لە AndroidManifest.xmlدا لەناویشیدا دەبێت Premissionی BIND\_INPUT\_METHOD وەربگرێت, وە هەروەها لە وەڵامی ئەو کردارەشدا android.view.InputMethod دابنرێت. ئەوەی لە نێوان هەردوو تاگی Application دایە، ئەسڕینەوە و ئەم کۆدە دادەنێین:

    <service android:name=".keyboard_androkurd"
        android:label="@string/app_name"
        android:permission="android.permission.BIND\_INPUT\_METHOD">
        <meta-data android:name="android.view.im" android:resource="@xml/method"/>
        <intent-filter>
            <action android:name="android.view.InputMethod" />
        </intent-filter>
    </service>

### **٤. دروستکردنی Method.xml**

لە پەڕگەی Manifest و تاگی Service ئەگەر سێربکەن لە ناو تاگی meta-dataدا، Method.xmlمان وەک سەرچاوە بەکاربردووە، ئەگەر بێت و ئەم پەڕگەیە دروست نەکەین، ئەوا لەکاتی کارپێکردنیدا سیستەمەکە هەڵەمان نیشان دەدات. ئەم پەڕگەییە زانیاریەکانی تایبەت بە تەختەکلیلەکەی لە خۆگرتووە یەکەم ناساندنی وەک Input Methodێک (تەختەکلیلێک)، دووەم subtypesکەی (ژێرناوی تەختەکلیلەکە). بۆ تەختەکلیلێک، subtypeکەی بنووسین **en_US،** ئەوا بوخچەیەک دروست دەکەین لە res بەناوی **XML**  ئەگەر نەبوو، وە لە ناویدا پەڕگەیەک بەناوی Method.xml دروست دەکەین، ئەمەی تێدا دادەنێین کە نموونەی ڕوونکردنەوەی سەرەوەیە بەشێوەی کۆد:

    <?xml version="1.0" encoding="utf-8"?>
    <input-method xmlns:android="http://schemas.android.com/apk/res/android">
    <subtype
        android:label="@string/subtype\_ku\_en"
        android:imeSubtypeLocale="en_US"
        android:imeSubtypeMode="keyboard_androkurd" />
    </input-method>

### **٥. دەسکاریکردنی strings.xml**

پەڕگەی Strings دەکەوێتە ئەم ڕێچکەیەوە res/values/strings.xml، لە پاش چوون ئەم سێ کۆکراوەیەی دەقە زیاد دەکەین، کە بەکارمان هێناوە لە ناونانی نەرمەواڵە و تەختەکلیلەکە.

+   یەکەم: ناوی نەرمەواڵەکەیە.
+   دووەم: ناوی تەختەکلیلەکەیە.
+   سێیەم: ژێرناوی تەختەکلیلەکەیە.

پەڕگەی Strings.xml نوێبکەوە، بەم شێوەیە:

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string name="app\_name">Androkurd\_Keyboard</string>
        <string name="keyboard\_ime">AndoKurd\_Key</string>
        <string name="subtype\_ku\_en">kurdish And english</string>
    </resources>

### **٦. پێناسکردنی نەخشەی تەختەکلیل**

نەخشەی تەختەکلیل (keybaoard) تەنها لە ڕێگای KeyboardView دەبێت. وە layout_alignParentBottom بۆ دادەنێین وە ئاماژە بە true دەکەین، تا ئەوەی نەخشەکە لە خواروودا جێگیر بێت، کاتێک نیشان دەدرێت. کاتێک پڕۆژەکەمان دروست کرد ناویی layoutکەمان نا keyboard.xml وەک و لە هەنگاوی یەک ئاماژەمان دا، دەچینە ناوی، کۆدەکانی ناوی هەمووی دەسڕینەوە و ئەمەی لە جێدا دادەنێین:

    <?xml version="1.0" encoding="UTF-8"?>
    <android.inputmethodservice.KeyboardView
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/keyboard"
        android:layout\_width="match\_parent"
        android:layout\_height="wrap\_content"
        android:layout_alignParentBottom="true"
        android:keyPreviewLayout ="@layout/preview"
        />

دواتر، وەک دەبینین لە keyPreviewLayout ئاماژەمان بە preview.xml کردووە، کە بریتییە لە شێوە دەرکەوتنی پیتەکان و ناوەکەیان. layoutکی بۆ دروست دەکەین لە res/layout/preview.xml و تەنها Textviewێکی تێدا دادەنێین تا ئەوەی پیتەکانی تێدا دەرکەوی،نموونەی کۆدیی:

    <?xml version="1.0" encoding="utf-8"?>
    <TextView xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout\_width="match\_parent"
        android:layout\_height="match\_parent"
        android:gravity="center"
        android:background="#ffff00"
        android:textStyle="bold"
        android:textSize="30sp">
    </TextView>

### **٧. پێناسکردنی پیتەکانی تەختەکلیل**

بریتییە لە پیتەکانی تەختەکلیل و شوێنی دەرکەوتنیان کە هەمووی لە پەڕگەیەکی XML جێبەجێ دەکەین. هەر پیتێک ئەم سیفاتەی دەبێت هەبێت:

+   **keyLabel**: ناوەڕۆکەکەی بریتییە لەو دەقەی کە نیشاندەدرێت لەکاتی کارپێکردنی تەختەکلیلەکە.
+   **codes**: ناوەڕۆەکەکەی بریتییە لە کۆدی پیتەکان بەشێوەی Unicode، کە دەبێتە نوێنەر بۆ پیتەکە.

بۆ نموونە: ئەگەر پیتی A دەرکەوێت و بنووسێت، لە Codesدا بۆ valueی دەنووسین 97 وە لە keyLabelیدا دەنووسین A. ئەگەر زیاتر لە پیتێک دابنێین و  بۆ هەموویان لە Codesدا بنووسین 97، ئەوا هەموو پیتەکان لە کاتی کرتەکردن لێیدا، دەنووسن A. بۆ نموونە: 3 خانە زیاد دەکەین و هەر سێکی KeyLabelی بریتیی بێت لە A بەڵام بە سێ Codesی جیاواز، کە ئامانەن **63**, **33**, وە **58**.

+   بۆ یەکەم لە کاتی کرتەکردندا، ئەمە ئەنجامەکەیەتی ?
+   بۆ دووەم لە کاتی کرتەکردندا، ئەمە ئەنجامەکەتی !
+   بۆ سێیەم لە کاتی کردتەکردندا، ئەمە ئەنجامەکەیەتی :

هەندێ سیفاتی تر، کە ئارەزوومەندانەیە بەکارهێینیان:

+   **keyEdgeFlags**: لەناویدا دەنووسرێت Right یان Left، واباوە تەنها بۆ ئەوانە دابنرێت کە دەکەونە لای ڕاست یان چەپی ڕیزێکەوە لە پیتەکان.
+   **keyWidth**: ئەم سیفاتە پانی پیتێک دیاری دەکات، وا باوە کە ڕێژەکە بە ڕێژەی سەدی بنووسرێت.
+   **isRepeatable**: بۆ ئەو پیتانە دادەنرێت کە دەست زۆر لەسەری بمێنێتەوە (نموونە وەک سڕینەوە و بۆشای دان کە پێویست دەکات دەستی لەسەر ڕابگیرێت بۆ سڕینەوەی کۆمەڵە پیتێک) ئەگەر ویست ئەم سیفاتە هەبێت ئەوا ture دادەنێیت.

پیتەکانی تەختەکیل بۆ هەر ڕیزێک، گروپێکی بۆ دادەنرێت، گونجاوە و ڕاهێنانی لەسەر بکە هەر ڕێزێک ١٠ دانە زۆرتر دامەنێ. هەر پیتێک وا گونجاوە کە پانیەکەی ڕێژەی 10% بۆ دابنرێ، لە ئاستی بەرزی هەر پیتێکیش واگونجاوە و وە پێشنیارکراوە کە بەرزی 48dp هەبێت. (بەهۆکاری ئەوەی ئێمە تەختەکلیلەمان ژمارەی لەگەڵدا دەبێت لە بەشی سەرەوەدا، ئەوا ٥ ستوون ڕیز دەکەین) بنچینە و ڕووکاری تەختەکلیلەکە بنیاد دەنێین، سەرەتا پەڕگەیەکی نوێ دروست بکە، بەناوی qwerty.xml لە بوخچەی res/xmlدا، کۆدەکانی بسڕەوە و ئەم کۆدەکانەی لە جێدا دانێ:

    <Keyboard xmlns:android="http://schemas.android.com/apk/res/android"
        android:keyWidth="10%p"
        android:horizontalGap="0px"
        android:verticalGap="0px"
        android:keyHeight="60dp"
        >
        <Row>
            <Key android:codes="0x661" android:keyLabel="١" android:keyEdgeFlags="left"/>
            <Key android:codes="0x662" android:keyLabel="٢"/>
            <Key android:codes="0x663" android:keyLabel="٣"/>
            <Key android:codes="0x664" android:keyLabel="٤"/>
            <Key android:codes="0x665" android:keyLabel="٥"/>
            <Key android:codes="54" android:keyLabel="6"/>
            <Key android:codes="55" android:keyLabel="7"/>
            <Key android:codes="56" android:keyLabel="8"/>
            <Key android:codes="57" android:keyLabel="9"/>
            <Key android:codes="48" android:keyLabel="0" android:keyEdgeFlags="right"/>
        </Row>
        <Row>
            <Key android:codes="113" android:keyLabel="q" android:keyEdgeFlags="left"/>
            <Key android:codes="119" android:keyLabel="w"/>
            <Key android:codes="101" android:keyLabel="e"/>
            <Key android:codes="114" android:keyLabel="r"/>
            <Key android:codes="116" android:keyLabel="t"/>
            <Key android:codes="121" android:keyLabel="y"/>
            <Key android:codes="117" android:keyLabel="u"/>
            <Key android:codes="105" android:keyLabel="i"/>
            <Key android:codes="111" android:keyLabel="o"/>
            <Key android:codes="112" android:keyLabel="p" android:keyEdgeFlags="right"/>
        </Row>
        <Row>
            <Key android:codes="97" android:keyLabel="a" android:keyEdgeFlags="left"/>
            <Key android:codes="115" android:keyLabel="s"/>
            <Key android:codes="100" android:keyLabel="d"/>
            <Key android:codes="102" android:keyLabel="f"/>
            <Key android:codes="103" android:keyLabel="g"/>
            <Key android:codes="0x647" android:keyLabel="ه"/>
            <Key android:codes="0x698" android:keyLabel="ژ"/>
            <Key android:codes="0x6a9" android:keyLabel="ک"/>
            <Key android:codes="0x644" android:keyLabel="ل"/>
            <Key android:codes="35,64" android:keyLabel="\\# \\@" android:keyEdgeFlags="right"/>
        </Row>
        <Row>
            <Key android:codes="-1" android:keyLabel="CAPS" android:keyEdgeFlags="left"/>
            <Key android:codes="0x632" android:keyLabel="ز"/>
            <Key android:codes="0x62e" android:keyLabel="خ"/>
            <Key android:codes="0x62c" android:keyLabel="ج"/>
            <Key android:codes="0x6a4" android:keyLabel="ڤ"/>
            <Key android:codes="0x628" android:keyLabel="ب"/>
            <Key android:codes="0x646" android:keyLabel="ن"/>
            <Key android:codes="0x645" android:keyLabel="م"/>
            <Key android:codes="46" android:keyLabel="."/>
            <Key android:codes="63,33,58" android:keyLabel="\\? ! :" android:keyEdgeFlags="right"/>
        </Row>
        <Row android:rowEdgeFlags="bottom">
            <Key android:codes="44" android:keyLabel="," android:keyWidth="10%p"  android:keyEdgeFlags="left"/>
            <Key android:codes="47" android:keyLabel="/" android:keyWidth="10%p" />
            <Key android:codes="32" android:keyLabel="بۆشای" android:keyWidth="40%p" android:isRepeatable="true"/>
            <Key android:codes="-5" android:keyLabel="سڕینەوە" android:keyWidth="20%p" android:isRepeatable="true"/>
            <Key android:codes="-4" android:keyLabel="باشە" android:keyWidth="20%p" android:keyEdgeFlags="right"/>
        </Row>
    </Keyboard>

ئەگەر تێبینی بکەیت، دەبینیت هەندێک لە پیتەکان لە Codes بەهای سالب لەگەڵ دانراوە، ئەم پیتانە بەهای نەگۆڕیان هەیە، بۆ نموونە دوگمەی (سڕینەوە) بەهای 5- کە ئاماژەییە بە (Keyboard.KEYCODE_DELETE) سەرجەم پیتە کوردیەکان بەشێوەی Unicode لێرەیە: **[کرتە بکە بە شێوەی PDF](http://unicode.ekrg.org/download/UnifiedKeyboardProject_enGB.pdf)** تێبینی: هەر پیتێک کە کۆدی یونیکۆدەکەی وەردەگرین بۆ خانەی Codes تەنها ٣ ژمارەی ئاخیری وەردەگرین دوای ژمارە 0 پیتی x دادەنێین. بۆ نموونە ئەگەر کۆدی یونیکۆدی ژمارە ١ (U+0661) بگۆڕین بۆ Codes ئەوا بەم شێوەی لێدەکەین 0x661، وە بۆ هەموو پیتەکانی تریش.

### **٨. دروستکردنی Classی Service**

ئەگەر بیرتان بێت لە سەرەتادا ناوی پەڕگەکەمان نا (keyboard\_androkurd.java)، ئێستا دەسکاری دەکەین، درێژی دەکەینەوە بۆ (InputMethodService) ئەویش Implementی (OnKeyboardActionListener)ی دەدەینێ، کە ئەمە کاریی ئەوەییە چالاکی پیتەکان بانگ دەکات، کاتێک کرتە یاخوود دەستی ڕادەگرین لەسەر پیتەکان. Classی keyboard\_androkurd ٣ variables لەخۆدەگرێت، کە ئامانەن:

+   KeyboardView: پێناسەکردن یاخوود ئاماژەکردنە بۆ شێوە دەرکەوتنی Layout
+   Keyboard: شێوازەکان بۆ دەرکەوتی KeyboardViewییە.
+   boolean: بەکاردەهێنین بۆ Caps (واتە بۆ کەپیتاڵ و سمۆڵی پیتەکانی ئینگلیزی) بۆیی کاتێک ON بوو، پیتەکان لە سمۆڵەوە بگۆڕێت بۆ کەپیتەڵ.

ئەنجامی وتەکانی سەرەوە بە شێوەی کۆد:

    public class keyboard_androkurd extends InputMethodService
            implements KeyboardView.OnKeyboardActionListener {\
        private KeyboardView kv;
        private Keyboard keyboard;
    
        private boolean caps = false;
    
        @Override
        public void onKey(int primaryCode, int\[\] keyCodes) {
    
        }
        
        @Override
        public void onPress(int primaryCode) {
        }
    
        @Override
        public void onRelease(int primaryCode) {
        }
    
        @Override
        public void onText(CharSequence text) {
        }
    
        @Override
        public void swipeDown() {
        }
    
        @Override
        public void swipeLeft() {
        }
    
        @Override
        public void swipeRight() {
        }
    
        @Override
        public void swipeUp() {
        }
    }

پێویستە دەکات بانگی Methodی **onCreateInputView** بکەین بۆ دەرکەوتنی ئەوانەی کردوومانە بۆ تەختەکلیلەکە، هەموو ئەو variablesنەی دروستمان کرد لێرەدا بەکاریان دەهێنین، کۆدەکانی سەرەوە دەسکاری دەکەین و نوێیدەکینەوە لە ناو کڵاسەکەمان و دوای implements ئەمە زیاد دەکەین:

    @Override
    public View onCreateInputView() {
        kv = (KeyboardView)getLayoutInflater().inflate(R.layout.keyboard, null);
        keyboard = new Keyboard(this, R.xml.qwerty);
        kv.setKeyboard(keyboard);
        kv.setOnKeyboardActionListener(this);
        return kv;
    }

**دواتر،** ئەگەر بمانەوێت لە کاتی کرتە کردن لە پیتەکان دەنگێک بێت، ئەوا پێویستە سوود لە Classی AudioManger وەربگرین بۆ کارکردنی دەنگەکە، لە Android SDKدا بەشێوەیەکی ئاسای کاتێک بتەوێت ئەم کاریگەرییە ببەخشیت ئەوا Methodی playClick بەکاردەهێنرێت. (ئەم کۆدانە دوایی onKey زیاد بکە)

    private void playClick(int keyCode){
        AudioManager am = (AudioManager)getSystemService(AUDIO_SERVICE);
        switch(keyCode){
            case 32:
                am.playSoundEffect(AudioManager.FX\_KEYPRESS\_SPACEBAR);
                break;
            case Keyboard.KEYCODE_DONE:
            case 10:
                am.playSoundEffect(AudioManager.FX\_KEYPRESS\_RETURN);
                break;
            case Keyboard.KEYCODE_DELETE:
                am.playSoundEffect(AudioManager.FX\_KEYPRESS\_DELETE);
                break;
            default: am.playSoundEffect(AudioManager.FX\_KEYPRESS\_STANDARD);
        }
    }

**کۆتایی**، ئێستا دەسکاری methodی onKey دەکەین و نوێی دەکەینەوە، پەیوەندیەک دروست دەکەین لە نێوان input filedکانی (خانەکانی) نەرمەواڵەکانی تر و تەختەکلیلەکە. **getCurrentInputConnection**: جۆرە Methodێکە بەکاردەهێنرێت بۆ بەکارهێنانی وەرگرتنەوەی پەیوەندییەک لە input filedی (خانەکانی) نەرمەواڵەکانی تردا، چەند جۆرێک هەن:

+   commitText: بۆ زیادکردنی پیتێک یان زیاتر لە یەک پیت لە خانەیەکدا.
+   deleteSurroundingText: سڕینەوەی پیتێک یان زیاتر لە یەک پیت لە خانەیەکدا.
+   sendKeyEvent: بۆ ناردنی ڕووداوێکە، نموونە KEYCODE_ENTER، لە هەر نەرمەواڵەیەکی دەرەکیدا.

لەهەر کاتێکدا بەکاربەر کرتە دەکات لە پیتێک، ئەوا لە ڕێگای methodی onKey پەیوەندی دەکرێت بە یونیکۆدی پیتەکان، بەڵام هەندێک هۆکاری تریش هەن، نموونە:

+   ئەگەر کۆدەکە بریتیی بوو لە KEYCODE_DELETE ئەوا لە ڕێگای Methodی deleteSurroundingText پیتەکان دەسڕێتەوە،
+   ئەگەر کۆدەکە بریتیی بوو لە KEYCODE\_DONE یان KEYCODE\_ENTER ئەوا جۆرێکن لە event.
+   ئەگەر کۆدەکە بریتیی بوو لە KEYCODE_SHIFT، ئەوا بەکاردەهێنرێت بۆ حاڵەتی گۆڕین، نموونە پیتی Caps کە پیتەکان لە سمۆڵەوە دەگۆڕێت بۆ کەپیتەڵ و بە پێچەوانەوە. (سوود لە Methodی invalidateAllKeys وەردەگرێت)
+   هەموو کۆدەکانی تر بەشێوەیەکی ئاسایی دەگۆڕین بۆ پیتێک و دەنێرێن بۆ Input fieldکان.

نێوانی Methodی onKey نوێبکەوە، بۆ ئەمە (کە نموونەی کۆدە بۆ قسەکانی سەرەوە):

    @Override
    public void onKey(int primaryCode, int\[\] keyCodes) {
        InputConnection ic = getCurrentInputConnection();
        playClick(primaryCode);
        switch(primaryCode){
            case Keyboard.KEYCODE_DELETE :
                ic.deleteSurroundingText(1, 0);
                break;
            case Keyboard.KEYCODE_SHIFT:
                caps = !caps;
                keyboard.setShifted(caps);
                kv.invalidateAllKeys();
                break;
            case Keyboard.KEYCODE_DONE:
                ic.sendKeyEvent(new KeyEvent(KeyEvent.ACTION\_DOWN, KeyEvent.KEYCODE\_ENTER));
                break;
            default:
                char code = (char)primaryCode;
                if(Character.isLetter(code) && caps){
                    code = Character.toUpperCase(code);
                }
                ic.commitText(String.valueOf(code),1);
        }
    }

### **تاقیکردنەوەی تەختەکلیلەکە**

دوایی ئەوەی هەموو شتێکمان بە سەرکەوتووی دروستکرد وەک ڕوونکردنەوەکە، پڕۆژەکەمان تاقیدەکینەوە و چێژ لە سەرکەوتنی کارەکەمان دەبینین: (بیرتان بێت بۆ تاقیکردنەوەی پڕۆژەکە سوود لە ئەندرۆیدی وەهمی وەردەگرین) پڕۆژەی ئەم جارەمان لە کاتی دامەزراندنیدا نیشان نادرێت، چونکە هیچ جۆرە Activityکمان بۆ دروست نەکردووە، بۆییە دەبێت بچینە Settings و خۆمان تەختەکلیلەکە چالاک بکەین، بەم شێوەیە: 

![androkurd_keboard](https://user-images.githubusercontent.com/42367292/44075406-6405c920-9fa5-11e8-89d7-47d1faac5a7f.png) 

**دواتر**، کاتێک چالاکمان کرد و هەڵمان بژارد وەک تەختەکلیلی سەرەکی، دەچینە هەر نەرمەواڵیەک کە بمانەوێت و تاقیکاری دەکەین (بۆ نموونە هەر نەرمەواڵەکی نامە ناردن) کرتە دەکەین لە Input Filedێک(خانەیەک) تا تەختەکلیلەکە دەربکەوێت، وە دەتوانییت بنووسیت و تاقیکاری بکەیت، ببێتە سەرەتایەکی گەشاوە بۆ دروستکردنی دانایەکی باشتر و بەتایبەتمەندتر هەروەک ئەوەیی خۆت خواستی بنیادنانتە، نموونە: 

![androkurd_keyboard_1](https://user-images.githubusercontent.com/42367292/44075451-7e343016-9fa5-11e8-993b-68fcc3933c62.png)

### **داگرتنی پڕۆژەکە:**

+   [بۆ تاقیکردنەوە (APK)](http://www.webchinupload.com/f/2018-08/54d85f7f7b544820466efc56770c3b0d.apk)

>  سووپاس، سەرکەوتووبن.
> 
