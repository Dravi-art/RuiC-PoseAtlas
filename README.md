# RuiC-PoseAtlas 鑷缓閮ㄧ讲鎵嬪唽

> 杩欎唤鏄?*鎴戜滑鑷繁鐨?*鎿嶄綔鎵嬪唽锛屼笉鏄綔鑰呯殑 README銆備綔鑰呴偅浠借鐨勬槸椤圭洰鏈韩锛岃繖浠借鐨勬槸**浣犳€庝箞鎶婂畠璺戣捣鏉ャ€佹€庝箞鏇存柊銆佹€庝箞鎹㈠湴鏂归儴缃?*銆?
## 鐜扮姸

- 绔欑偣锛歨ttps://poseatlas-18h.pages.dev
- Cloudflare 椤圭洰鍚嶏細`poseatlas`
- Cloudflare 璐﹀彿锛?416858007@qq.com
- 鏈湴瀹屾暣浠撳簱锛歚E:\AI\poseatlas`
- 鏈湴閮ㄧ讲鍓湰锛歚E:\AI\deploy`
- GitHub 浠撳簱锛歨ttps://github.com/Dravi-art/RuiC-PoseAtlas锛堝彧鏀句唬鐮侊紝涓嶅惈鍘熷浘锛?
## 鐩綍璇存槑

| 璺緞 | 鍐呭 | 鑳戒笉鑳藉垹 |
|---|---|---|
| `E:\AI\poseatlas` | 瀹屾暣浠撳簱锛氫唬鐮?+ 濮垮娍/琛ｈ/浜哄儚鍏ㄩ儴鍘熷浘 + `.git` | 寤鸿淇濈暀 |
| `E:\AI\deploy` | 閮ㄧ讲鍓湰锛氬悓鍐呭浣嗕笉鍚?`.git` | 鍙垹锛岃兘閲嶆柊鐢熸垚 |
| `E:\AI\src` | 涓変釜绱犳潗鍖呰В鍘嬪嚭鏉ョ殑鍘熷浘 | 鍙垹锛岃兘閲嶆柊瑙ｅ帇 |
| `E:\AI\*.zip` | 鍘熷绱犳潗鍖咃紙濮垮娍/琛ｈ/鑴稿簱锛?| 鍙垹锛岀綉鐩樿繕鑳戒笅 |

## 鏃ュ父鏇存柊锛堜綔鑰呮洿鏂颁簡浠撳簱锛?
浣滆€呬粨搴擄細https://github.com/HRuiCcc/RuiC-PoseAtlas

```powershell
cd E:\AI\poseatlas
git remote add upstream https://github.com/HRuiCcc/RuiC-PoseAtlas.git   # 鍙渶绗竴娆?git fetch upstream
git merge upstream/main
```

鍚屾鍒伴儴缃茬洰褰曪紙鎺掗櫎 `.git`锛夛細

```powershell
robocopy E:\AI\poseatlas E:\AI\deploy /E /XD .git /NFL /NDL /NJH /NJS /NP
```

閲嶆柊閮ㄧ讲锛?
```powershell
set CLOUDFLARE_API_TOKEN=<你的 Cloudflare API Token>
C:\Users\Administrator\AppData\Roaming\npm\wrangler.cmd pages deploy E:\AI\deploy --project-name poseatlas --branch main
```

## 浠庨浂寮€濮嬶紙鎹㈡満鍣?/ 閲嶈锛?
### 1. 鎷夊彇浣滆€呬粨搴?
```powershell
git clone https://github.com/HRuiCcc/RuiC-PoseAtlas.git E:\AI\poseatlas
```

### 2. 涓嬭浇绱犳潗鍖?
鐢ㄨ嚜宸辩殑澶稿厠锛歨ttps://pan.quark.cn/s/65cfb059ee71?pwd=9u9S

鍘熶綔鑰呭じ鍏嬬綉鐩橈細https://pan.quark.cn/s/d775c1471804?pwd=Ahcd
鎻愬彇鐮侊細`Ahcd`

涓変釜鍖咃細
- `AI 浣滃浘濮垮娍搴?zip`锛堢害 630MB锛?- `AI 鏈嶈搴?zip`锛堢害 1.3GB锛?- `AI 浣滃浘鑴稿簱.zip`锛堢害 4.6GB锛?
### 3. 瑙ｅ帇

```powershell
7z x "AI 浣滃浘濮垮娍搴?zip" -oE:\AI\src\pose
7z x "AI 鏈嶈搴?zip" -oE:\AI\src\costume
7z x "AI 浣滃浘鑴稿簱.zip" -oE:\AI\src\face
```

### 4. 鍚堝苟鍥剧墖杩涗粨搴?
| 绱犳潗 | 鏉ユ簮 | 鐩爣 |
|---|---|---|
| 濮垮娍 | `E:\AI\src\pose\originals\*.png` | `E:\AI\poseatlas\img\` |
| 琛ｈ | `E:\AI\src\costume\originals\*.png` | `E:\AI\poseatlas\costume\img\`锛堜粨搴撹嚜甯?webp锛宲ng 鍙€夛級 |
| 浜哄儚 | `E:\AI\src\face\originals\*.png` | `E:\AI\poseatlas\portrait\img\` |

**浜哄儚杩欎竴姝ュ繀椤诲仛**锛氫綔鑰呬粨搴撻粯璁や笉鍖呭惈浜哄儚鍘熷浘锛坄.gitignore` 蹇界暐浜?`portrait/img/`锛夛紝涓嶆嫹杩涘幓浜哄儚椤电偣寮€澶у浘鏄┖鐨勩€?
### 5. 鐢熸垚閮ㄧ讲鍓湰

```powershell
robocopy E:\AI\poseatlas E:\AI\deploy /E /XD .git /NFL /NDL /NJH /NJS /NP
```

### 6. 瀹夎 wrangler

```powershell
npm install -g wrangler
```

### 7. 閮ㄧ讲

```powershell
set CLOUDFLARE_API_TOKEN=<你的 Cloudflare API Token>
C:\Users\Administrator\AppData\Roaming\npm\wrangler.cmd pages deploy E:\AI\deploy --project-name poseatlas --branch main
```

閮ㄧ讲瀹屼細杈撳嚭涓€涓?`https://xxxx.poseatlas-18h.pages.dev` 鐨勫湴鍧€銆?
## Cloudflare 鍑嵁

- API Token锛歚<你的 Cloudflare API Token>`
- 鏉冮檺锛欳loudflare Pages 鈫?Edit
- 璐﹀彿锛?416858007@qq.com
- 椤圭洰鍚嶏細`poseatlas`
- 鐢熶骇鍩熷悕锛歨ttps://poseatlas-18h.pages.dev

Token 杩囨湡鎴栬鎹細鐧诲綍 https://dash.cloudflare.com 鈫?鍙充笂瑙掑ご鍍?鈫?My Profile 鈫?API Tokens 鈫?Create Token 鈫?閫?Cloudflare Pages Edit銆?
## 甯歌闂

### push 鍒?GitHub 澶辫触锛坄did not receive expected object`锛?
GitHub 鍗曟 push 涓婇檺绾?2GB锛屽畬鏁翠粨搴?5.4GB 鎺ㄤ笉涓婂幓銆傜綉缁滀笉绋虫椂 800MB 涔熶細鏂€?**鍥剧墖涓嶉渶瑕佽繘 GitHub**鈥斺€斿畠浠湪 Cloudflare 涓娿€侴itHub 鍙斁浠ｇ爜锛?1GB锛夊氨澶熶簡銆?
### 閮ㄧ讲鍚?522 閿欒

Cloudflare 鍒版簮绔欒秴鏃躲€傛鏌ラ儴缃茬洰褰曢噷鏄笉鏄贩杩涗簡 `.git`锛堜細瀵艰嚧涓婁紶鍑犲崈涓?git 瀵硅薄鏂囦欢锛夈€?**蹇呴』鐢?`E:\AI\deploy`锛堜笉鍚?`.git`锛夐儴缃?*锛屼笉瑕佺洿鎺ラ儴缃?`poseatlas`銆?
### 鏇存柊鍚庡浘鐗囦涪澶?/ 浜哄儚椤电┖鐧?
浣滆€呬粨搴撶殑 `.gitignore` 榛樿蹇界暐 `portrait/img/`銆俙git pull` 涔嬪悗妫€鏌ヤ竴涓嬭繖涓洰褰曡繕鍦ㄤ笉鍦紝涓嶅湪灏变粠 `E:\AI\src\face\originals\` 閲嶆柊鎷枫€?
### 鎯虫崲鍩熷悕

Cloudflare Pages 鍏嶈垂缁?`*.pages.dev` 瀛愬煙鍚嶏紝涓嶇敤涔板煙鍚嶃€傛兂鐢ㄨ嚜宸辩殑鍩熷悕锛欳loudflare Pages 鈫?椤圭洰 鈫?Custom domains 鈫?娣诲姞銆?
## 绔欑偣缁撴瀯

- 濮垮娍鍥鹃壌锛歚/`
- 琛ｈ鍥鹃壌锛歚/costume.html`
- 浜哄儚鍥鹃壌锛歚/face.html`

## 涓€鍙ヨ瘽鎬荤粨

**閮ㄧ讲 = `E:\AI\deploy` 鐩綍 + wrangler + Cloudflare token銆?* 鍥剧墖鍦?Cloudflare 涓婏紝浠ｇ爜鍙互鏀?GitHub 澶囦唤銆傛洿鏂板氨鏄?`git pull` 鈫?`robocopy` 鈫?`wrangler deploy` 涓夋銆?
