# Mac 使用 OBS 直播

## OBS

开源、全平台最好的直播串流软件之一。

- 开源意味着更多人维护，更新快、性能好、bug较少
- 支持的功能能够覆盖直播推流的所有需求

注：如果是Windows电脑可以直接使用Bilibili官方的`直播姬`进行直播推流，使用体验没得说

### 安装OBS

官网下载 <https://obsproject.com>

Mac电脑选择macOS版本下载

下载好之后将软件拖动到电脑的应用程序文件夹即可

### 设置语言

打开软件之后，右下角可以进入设置，或者使用快捷键 ⌘, ，然后设置语言

### OBS简单使用

直播是什么：把声音和画面混合在一起 将音视频诗句传输至B站直播服务器

`Scene` `Source` `Audio Mixer` `Controls`

`Scene 场景`

- 一整个开播的场景
    - 比如平日开发代码直播是一种
    - 直播iPad打原神是一种
    - 和别的同学联动聊天的界面是一种
    - 歌回的界面是一种
- 不同场景中的声音和画面不同，使用的组件和UI不同

`Source 源`

- 主要
    - `Video Capture Device 视频捕捉`
        - 用来接入摄像头或iPad画面
        - `QuickTime Player` 也可以捕获iPad界面，性能更好，但稍微有一点延迟
    - `Display Capture 显示器捕捉` 
        - 主要用来捕捉Mac的屏幕
        - 如果有外接显示器可以将OBS放到外接显示器上，然后捕捉主显示器（反过来也可以）
    - `Window Capture 应用窗口捕捉`
        - 比如显示正在播放的音乐可以捕捉 `Music.app` 的界面
    - `Browser 浏览器捕捉`
        - 只要是浏览器的界面 都可以通过输入链接进行捕获
    - `Audio Input Capture 音频捕捉`
        - 音源：
            - 电脑发出的声音（提示音 网页播放的视频声音 音乐软件播放的声音）
            - 外置麦克风的声音
        - 推流：
            - 直播观众需要听到的声音
            - 需要调整不同音源的音量
        - 音响：
            - 联动时需要听到别人的声音
            - 电脑播放视频或音乐的时候自己也想听到
- 次要
    - `Image 图像`
        - 放静态图片当背景或插画
    - `Text 说明文字`
        - 放一些直播的说明
    - `Media Source 媒体（视频、音频等）`
        - 比如开场动画和需要播放的视频
- Group用来分组
    - 注意不支持嵌套组
    - 使用 `Scene 场景` 管理不同的页面是官方更推荐的方法

`Audio Mixer 混音器`

- 主要用来调声音 需要观众帮忙确认声音大小
- `右键 > Filter > Noise Suppression > 选择一种降噪方式`

### 视频设置

- 绿幕抠像：对于输入的视频源，`右键 > Filter > 左下角加号 > Chroma Key` 选择绿色、拖动滑动条选择抠掉绿色的程度
- 在OBS上选择其他画面
    - 思路：
        - 使用OBS支持的脚本设置文本框的文本
        - 使用浏览器捕获窗口
    - 在屏幕上显示当前日期：见附录
    - 在屏幕上显示B站弹幕：
        - <https://comen.app> 输入直播间的id就可以进行直播间弹幕的捕获。
        - 问题是背景不是透明的 还在开发中
        - [GitHub | 3Shain - Comen](https://github.com/3Shain/Comen)

### 音频设置

- 目标：耳机听到系统发出的声音，自己的语音和耳机听到的声音推流到观众端
- 设置方法：
    - 在<https://github.com/ExistentialAudio/BlackHole>下载 `BlackHole` 并按照说明进行安装（安装好后 系统的声音会通过这个BlackHole的管道 到达BlackHole的输出；macOS是不能录制Mac内部发出的声音的（音乐版权保护））
    - 打开macOS中的 `Audio MIDI Setup.app`，点击左下角加号添加多输出设备，添加耳机和BlackHole，Mac内部的音量需要既输出到耳机，又输出到BlackHole
    - 然后打开系统设置，在 `Sound 音频` 中选择输出设备为刚才创建的多输出设备。输入选择外置麦克风（注意如果使用AirPods 不要同时将AirPods作为输入和输出 音质会特别差）
    - 打开OBS，在 `Source 源` 处添加输入音频
        - 外置麦克风
        - BlackHole 因为创建了多输出设备 所以你耳机中听到的声音和BlackHole输入进OBS的声音是一致的

### Controls 设置

- `Stream 串流` 
    - 打开 `Bilibili直播中心 > 我的直播间 > 开播设置`，复制服务器地址和串流密钥到OBS设置中。点击开始串流即可开始直播。
- `Output 输出`
    - 输出码率根据上传网速选择 比如我家的上传网速最高是 2 MB/s，折算为 16000kbps，那么码率最高设置这么高
    - 码率越高压缩越少、画质越好；但需要考虑设备性能
- `Audio 音频`
    - 全局音频全部关掉 使用 `Source 源` 进行捕获即可
    - 采样率调到48kHz（最高音质 音频占不了多少存储）
- `Video 视频`
    - 注意如果设备GPU和网络性能不是特别好的话好把帧率和分辨率调低一些
- `Hotkeys 快捷键`
    - 比如你要快速开麦、放一些图可以使用快捷键操作；按自己的需求来
- `Advanced 高级`
    - 一般不用动 如果只是使用的话

## 附

### OBS时间显示 脚本

lua脚本是不需要安装额外解析程序的，可以直接在OBS的菜单栏选择脚本设置参数进行使用。

`菜单栏 > Tools > Scripts` 点击左下角加号添加时间脚本，按照下面的方式设置参数。因为要分两行显示，所以可以创建两个相同的脚本：

- `current_date.lua` `%a %b %d` `Mon Feb 07`
- `current_time.lua` `%X` `20:21:05`

```lua
--[[ OBS Studio datetime script

This script transforms a text source into a digital clock. The datetime format
is configurable and uses the same syntax than the Lua os.date() call.
]]

obs             = obslua
source_name     = ""
datetime_format = ""

activated       = false

-- Function to set the time text
function set_datetime_text(source, format)
	local text = os.date(format)
	local settings = obs.obs_data_create()

	obs.obs_data_set_string(settings, "text", text)
	obs.obs_source_update(source, settings)
	obs.obs_data_release(settings)
end

function timer_callback()
	local source = obs.obs_get_source_by_name(source_name)
	if source ~= nil then
		set_datetime_text(source, datetime_format)
		obs.obs_source_release(source)
	end
end

function activate(activating)
	if activated == activating then
		return
	end

	activated = activating

	if activating then
		obs.timer_add(timer_callback, 1000)
	else
		obs.timer_remove(timer_callback)
	end
end

-- Called when a source is activated/deactivated
function activate_signal(cd, activating)
	local source = obs.calldata_source(cd, "source")
	if source ~= nil then
		local name = obs.obs_source_get_name(source)
		if (name == source_name) then
			activate(activating)
		end
	end
end

function source_activated(cd)
	activate_signal(cd, true)
end

function source_deactivated(cd)
	activate_signal(cd, false)
end

function reset()
	activate(false)
	local source = obs.obs_get_source_by_name(source_name)
	if source ~= nil then
		local active = obs.obs_source_showing(source)
		obs.obs_source_release(source)
		activate(active)
	end
end

----------------------------------------------------------

function script_description()
	return "Sets a text source to act as a clock when the source is active.\
\
The datetime format can use the following tags:\
\
    %a	abbreviated weekday name (e.g., Wed)\
    %A	full weekday name (e.g., Wednesday)\
    %b	abbreviated month name (e.g., Sep)\
    %B	full month name (e.g., September)\
    %c	date and time (e.g., 09/16/98 23:48:10)\
    %d	day of the month (16) [01-31]\
    %H	hour, using a 24-hour clock (23) [00-23]\
    %I	hour, using a 12-hour clock (11) [01-12]\
    %M	minute (48) [00-59]\
    %m	month (09) [01-12]\
    %p	either \"am\" or \"pm\" (pm)\
    %S	second (10) [00-61]\
    %w	weekday (3) [0-6 = Sunday-Saturday]\
    %x	date (e.g., 09/16/98)\
    %X	time (e.g., 23:48:10)\
    %Y	full year (1998)\
    %y	two-digit year (98) [00-99]\
    %%	the character `%´"
end

function script_properties()
	local props = obs.obs_properties_create()

	obs.obs_properties_add_text(props, "format", "Datetime format", obs.OBS_TEXT_DEFAULT)

	local p = obs.obs_properties_add_list(props, "source", "Text Source", obs.OBS_COMBO_TYPE_EDITABLE, obs.OBS_COMBO_FORMAT_STRING)
	local sources = obs.obs_enum_sources()
	if sources ~= nil then
		for _, source in ipairs(sources) do
			source_id = obs.obs_source_get_id(source)
			if source_id == "text_gdiplus" or source_id == "text_ft2_source" then
				local name = obs.obs_source_get_name(source)
				obs.obs_property_list_add_string(p, name, name)
			end
		end
	end
	obs.source_list_release(sources)

	return props
end

function script_defaults(settings)
	obs.obs_data_set_default_string(settings, "format", "%X")
end

function script_update(settings)
	activate(false)

	source_name = obs.obs_data_get_string(settings, "source")
	datetime_format = obs.obs_data_get_string(settings, "format")

	reset()
end

function script_load(settings)
	local sh = obs.obs_get_signal_handler()
	obs.signal_handler_connect(sh, "source_show", source_activated)
	obs.signal_handler_connect(sh, "source_hide", source_deactivated)
end
```
