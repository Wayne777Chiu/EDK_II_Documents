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

Note: _<Usage Block>_ 於變數區段裡伴隨著雙井字符`##`開始且**不**當成注釋，將用來被解析給 EDK II base tools 專案裡的 Intel(R) UEFIPackaging Tool. 在注釋區塊裡的這種運用描述了協定(Protocol), PPIS 或 全區唯一識別碼(GUID)如何使用在C code.

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

### [Defines] <BR>

### [Packages]

### [Sources]

### [LibraryClasses]

### [Protocols]

### [Guids]

### [BuildOptions]

## DEC 檔

