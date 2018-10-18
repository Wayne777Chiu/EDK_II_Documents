# 建置描述檔 (Build Description Files)

>關於[本頁原始參照](https://github.com/tianocore/tianocore.github.io/wiki/Build-Description-Files)
>關於本頁原始參照最後編輯 -> Laurie Jarlstrom edited this page on 29 Jun 2017 · 1 revision 

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

Note: 有一種開頭使用雙井字符`##`的運用存在於在各種的區段內稱之為 _<Usage Block>_，而此時**不**當成注釋，而是將被用來解析給 EDK II base tools 專案裡的 Intel(R) UEFIPackaging Tool. 而在注釋區塊裡的這種運用描述了協定(Protocol), PPIS 或 全區唯一識別碼(GUID)如何使用於C code.

例:
> In \ArmPkg\Drivers\ArmPciCpuIo2Dxe\ArmPciCpuIo2Dxe.inf:
```
[Protocols]
  gEfiCpuIo2ProtocolGuid                         ## PRODUCES
```
例:
> In \ArmVirtPkg\Library\ArmVirtDxeHobLib\ArmVirtDxeHobLib.inf:
```
[Guids]
  gEfiHobListGuid                               ## CONSUMES  ## SystemTable
```

### [Defines] <br>
```
     INF_VERSION            = 1.25 
```
定義 目前INF 檔所支援的EDK II INF 規範的版本. <br><br>
``` 
    BASE_NAME             = NameOuputWithoutExtension
```
當編譯完成為最後的二元檔(.efi or .lib binary file,定義該模組(application, libarary, etc...)的輸出名稱. <br><br>
``` 
    MODULE_UNI_FILE        = NameOuput.uni
```
選擇式的條目可從標頭區段來決定(locate)一個 Unicode 格式的檔案.該檔可用來做在地化(localization)該模組的摘要(abstract)與描述(description).副檔名.uni 檔 必須相呼應於同目錄的 INF 檔. <br><br>
```
     FILE_GUID             = 11111111-2222-3333-4444-555555555555
```
此模組的獨特GUID.請看　http://www.guidgen.com/ <br><br>
```
     MODULE_TYPE           = USER_DEFINED
```
建置模組的類型.這包含了 UEFI_DRIVER, UEFI_APPLICATION, DXE_DRIVER等;若是編譯成函示庫，也可以是 BASE, USER_DEFINED等. <br><br>
```
       VERSION_STRING      = 1.0
```
開發者定義的模組版本(Major "." Minor number).<br><br>
```
       ENTRY_POINT         = MainFunctionName
```
假如模組不是函示庫類型，這個變數定義函數的執行進入點,相似於c code 的 main 函數.<br><br>
```
       LIBRARY_CLASS  = LibNameToReference | AllowedModuleType1 AllowedModuleType2 Etc . . .
```
如果模組是函示庫,這是用來讓建置系統知道的名稱,可用來被其他模組類型(a vertical bar and a list of space delimitated module types)使用.<br><br>
```
       CONSTRUCTOR         = LibInitializationFunction
```
如果模組是函示庫且需要在起始點(startup)做初始化,這個名稱的變數會指明函數名稱在模組主要進入點(main entry point)被呼叫前先呼叫該函數.<br><br>

### [Packages]

列出各式的封裝將用來給模組使用.這將告訴建置系統去尋找函示庫物件(函示庫裡的標頭檔), 平台組態資料庫(pcds), 全區唯一識別碼(GUIDs), 協定(Protocols), 和 PPIs (PEIM to PEIM Interface?)(PEIM: PEI Module?)透過不同封裝宣告檔(packages .DEC files).在封裝裡的副檔名 .DCS 檔不會被使用(誤植?? 應該是.DSC Files???). 一般來說最小需求的封裝是 MdePkg.dec.
```
      MdePkg/MdePkg.dec
```

### [Sources]

列出各式的原始碼及標頭檔用來使用在建置該模組.
``` 
      MyFile.h
      MyFile.c
```

### [LibraryClasses]

列出各式的函示庫使用和連結於模組.這值代表了該函示庫在自身的 INF 檔所用的名稱. 在這個區段裡(副檔名 INF 裡[LibraryClasses]區段)的進入點在副檔名DSC 裡的[LibraryClasses]區段都需要有相對應的進入點(entry).這是因為在[Packages]區段裡的封裝並沒有用來使用去決定函示庫模組的連結(link with).<br>
例:
``` 
   LibNameToReference
```

### [Protocols]

列出各式協定(Protocols)的通用識別碼(GUIDs)的變數名稱,該名稱被原始碼所使用或需要.這個變數被定義在封裝的 DEC 檔([Packages].DEC)的 [Guids]區段內.也會列上使用段定義(Usage Block definitions)上提供給這麼模組上的協定. <br>
例:
``` 
  gEfiDiskInfoProtocolGuid                      ## BY_START
```
這`## BY_START`是個關鍵詞

### [Guids]

### [BuildOptions]

## DEC 檔

