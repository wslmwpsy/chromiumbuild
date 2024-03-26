gclient sync --revision src@111.0.5563.148 --with_tags --with_branch_heads

set http_proxy=http://127.0.0.1:12377
set https_proxy=http://127.0.0.1:12377

set socks_proxy=scoks5://127.0.0.1:12377

git config --global http.proxy http://127.0.0.1:12377
git config --global https.proxy http://127.0.0.1:12377



git config --global user.name "wslmwpsy"
git config --global user.email "875295145@qq.com"
git config --global core.autocrlf false
git config --global core.filemode false
git config --global branch.autosetuprebase always

gclient config https://chromium.googlesource.com/chromium/src.git



You must install the "Desktop development with C+ +" component and the "FC/ATLsupport" sub-components.
You must have the version 10.0.20348.0 Windows 10 SDK installed.


报错信息
WARNING :shbyroces "git" "-c""core.deltaleaseacelinit2g" "clone" "--no--cheakout" "--progres" "https:/chronim go0glesource.com/chromim/src.git" "c:\src\chroim\_gcliet_src_84bjxzz” in c:\chromium failed; will retry after a short nap...

git -c core.deltaBaseCacheLimit=2g clone --no-checkout --progress https://chomium/googlesource.com/chromium/src.git C:\src\chromium\_gclient_src_kqfjauze

git -c core.deltaBaseCacheLimit=2g clone --no-checkout --progress https://chromium.googlesource.com/chromium/src.git C:\src\chromium\_gclient_src_2y276nlp

Q1:WARNING :shbyroces "git" "-c""core.deltaleaseacelinit2g" "clone" "--no--cheakout" "--progres" "https:/chronim googlesource.com/chromim/src.git" "c:\src\chroim\_gcliet_src_84bjxzz” in c:\chromium failed; will retry after a short nap...

A1：环境变量中需要做如下设
set DEPOT_TOOLS_UPDATE=0

Q2：gn.py: Could not find gn executable at: D:\workspace\chromium\src\buildtools\win\gn.exe

A2：环境变量中需要做如下设置（如下的2022可以改成2019）：
set DEPOT_TOOLS_WIN_TOOLCHAIN=0
set GYP_MSVS_VERSION=2022
set GYP_GENERATORS=ninja,msvs-ninja
set GYP_MSVS_OVERRIDE_PATH=C:\Program Files\Microsoft Visual Studio\2022\Enterprise

set GN_DEFINES=use_jumbo_build=true
set CEF_USE_GN=1
set DEPOT_TOOLS_UPDATE=0
set DEPOT_TOOLS_WIN_TOOLCHAIN=0


编译预处理生成解决方案"cef.sln"
Before your first reply, I tried a build with "set GN_DEFINES=is_official_build=true proprietary_codecs=true ffmpeg_branding=Chrome use_thin_lto=false chrome_pgo_phase=0" instead of adding "--with-pgo-profiles" to automate-git.py and it completed without errors, but if I understand the discussion topic that would be without the optimizations.

编译cef
src\mojo\public\tools\bindings\generators\mojom_ts_generator.py 
Here's how I managed to fix it:

  # Existing code in that function
  path = module.metadata.get('webui_module_path')

  # Add the below lines
  if path == '':
    path = '/'
  if path is None or path == '/':
    return path

  # Existing code in that function
  if _IsAbsoluteChromeResourcesPath(path):
Now, try rebuilding again. It should work

https://github.com/chromiumembedded/cef/commit/206b7b1c95a7624809c18db2622fe7b786765cf7

https://chromiumdash.appspot.com/releases?platform=Windows
https://chromiumdash.appspot.com/releases?platform=Linux