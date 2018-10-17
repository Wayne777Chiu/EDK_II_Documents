# 建置描述檔 (Build Description Files)

>關於[本頁原始參照](https://github.com/tianocore/tianocore.github.io/wiki/Build-Description-Files)

了解 副檔名DCS，DEC, 和 INF 建置描述檔的基本建立
其餘請參照最新版的 [[EDK II 規範]](https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Specifications)

***

 __**目錄**__
* [INF 檔](#the-inf-file) 模組資訊檔 (Module Information file) <BR>
   - [注釋](#comments) - [\[Defines\]](#defines) - [\[Packages\]](#packages) - [\[Sources\]](#sources) - [\[LibraryClasses\]](#libraryclasses) - [\[Protocols\]](#protocols) - [\[Guids\]](#guids) - [\[BuildOptions\]](#buildOptions)
* [DEC 檔](#the-dec-file) 封裝宣告檔 (Package Declaration file)<BR>
   - [注釋](#comments-1) - [\[Defines\]](#defines-1) - [\[Includes\]](#includes) - [\[LibraryClasses\]](#libraryclasses-1) - [\[Guids\]](#guids-1) - [\[Pcds . . .\]](#pcds-----sections)
* [DSC 檔](#the-dsc-file) 平台描述檔 (Platform Descrtiption File)<BR>
   - [\[Defines\]](#defines-2) - [\[LibraryClasses\]](#libraryclasses-2) - [\[Pcds . . .\]](#pcds-----sections-1) - [\[Components\]](#components) 

 ***

## INF 檔
對於規範及描述請看: [INF](https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Specifications#inf) 在 [[EDK II 規範]] 頁面<BR>
該檔案描述如何建置一個模組 (例如驅動程式(driver), 函式庫(library), 應用程式(application)等等...)。

### 注釋
單一`#`字符意旨在INF檔裡為注釋。在行內的注釋會中斷一行的碼；行內注釋必須處於行的最後，且儘可能不要放在一個區段([,])標籤(section tag)內。`#`井字符允許出現在引用的字串裡。

Note: _<Usage Block>_ 在變數區段裡有一種開頭使用雙井字符`##`的運用，這時**不**當成注釋，而是將被用來解析給 EDK II base tools 專案裡的 Intel(R) UEFIPackaging Tool. 而在注釋區塊裡的這種運用是描述了協定(Protocol), PPIS 或 全區唯一識別碼(GUID)如何使用於C code.

> In \MdePkg\Include\Library\PcdLib.h:
```
#define FeaturePcdGet(TokenName)            _PCD_GET_MODE_BOOL_##TokenName
```
> In \CryptoPkg\Library\OpensslLib\openssl\MdeModulePkg\Application\HelloWorld\HelloWorld.c:
```
...
 if (FeaturePcdGet (PcdHelloWorldPrintEnable)) {
 	...
```
> In \Build\NT32IA32\DEBUG_VS2015x86\IA32\MdeModulePkg\Application\HelloWorld\HelloWorld\DEBUG\AutoGen.h:
```
extern const  BOOLEAN  _gPcd_FixedAtBuild_PcdHelloWorldPrintEnable;
#define _PCD_GET_MODE_BOOL_PcdHelloWorldPrintEnable  _gPcd_FixedAtBuild_PcdHelloWorldPrintEnable
```

### [Defines] <br>
```
     INF_VERSION            = 1.25 
```
定義 目前INF 檔所支援的EDK II INF 規範的版本. <br><br>
``` 
    BASE_NAME             = NameOuputWithoutExtension
```
定義該模組(application, libarary, etc...)的輸出名稱,當編譯完成為最後的二元檔(.efi or .lib binary file). <br><br>
``` 
    MODULE_UNI_FILE        = NameOuput.uni
```
選擇式的條目可從標頭區段來決定(locate)一個 Unicode 格式的檔案.該檔可用來做在地化(localization)該模組的摘要(abstract)與描述(description).副檔名.uni 檔 必須相呼應於同目錄的 INF 檔. <br><br>
```
     FILE_GUID             = 11111111-2222-3333-4444-555555555555
```
獨特的GUID於此模組.請看　http://www.guidgen.com/ <br><br>
```
     MODULE_TYPE           = USER_DEFINED
```


### [Packages]

### [Sources]

### [LibraryClasses]

### [Protocols]

### [Guids]

### [BuildOptions]

## DEC 檔

