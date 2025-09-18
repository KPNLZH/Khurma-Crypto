# 🔒 Khurma Crypto

**Secure and blazing-fast AES-256 file encryption tool for all file types, powered by Rust.**  
**あらゆるファイル形式に対応した、高速かつ安全なAES-256ファイル暗号化ツール（Rust製）です。**

- This design philosophy enables a reproducible yet irreversible "controlled chaos", offering practical resistance even against quantum computers.

この設計思想により、再現可能かつ不可逆な“制御されたカオス”を実現し、量子コンピュータに対しても現実的に破られない耐性を提供します。

- By layering multiple rounds of encryption using arbitrary random seeds, the decryption key space expands to an astronomical scale, making brute-force attacks and quantum-assisted searches virtually infeasible.

任意の乱数シードから何重にも暗号化を重ねることで、復号の鍵空間は天文学的規模へと拡張され、総当たり攻撃や量子探索に対して極めて強靭です。


# 🧩 Binary Format Support / 対応フォーマット
This tool treats all files as binary (Vec<u8>), so it supports / 以下の形式に対応しています：

**Support format**
Any other format / その他すべての形式


## ✅ Use Cases / 主な用途

- **Safely storing files locally**  
  ローカルに安全にファイルを保存したいとき

- **Encrypting files for secure transfer or sharing**  
  暗号化してファイルを転送・共有したいとき

- **Protecting data in offline environments or on USB drives**  
  オフライン環境やUSBメモリでの情報保護
  
- **Add the executable to your environment PATH to easily call the command from other programs or scripts.**
　実行ファイルのパスを環境変数PATHに追加すれば、他のプログラムやスクリプトから簡単にコマンドを呼び出せます。

- **Perform multi-layer encryption using multiple passwords**  
  複数のパスワードを使った多重暗号化にも対応（連携ツールと組み合わせて利用可能）

This tool helps you keep your important files completely secure.  
あなたの大切なファイルをしっかり守ります。

---

## ⚙️ Features / 特徴

-  AES-256-CBC encryption with SHA-512 derived key and IV  
　AES-256-CBC方式＋SHA-512ベースの鍵/IV生成による強力な暗号化

-  Works with any file type: `.txt`, `.mp4`, `.zip`, `.exe`, and more  
　あらゆるファイル形式に対応（テキスト、動画、実行ファイルなど）
 
-  Chunked encryption for large files  
　大容量ファイルでも効率よく処理できるチャンク処理
 
-  Real-time progress display with processing speed  
　リアルタイム進捗表示＋処理速度表示

-  Rust-powered CLI: fast, secure, memory-efficient  
　Rustで実装された高速＆軽量なCLIツール

- A more user-friendly GUI (V1.2)
  より簡単な操作に対応したGUI (V1.2より実装)

- Compatible with the companion multi-layer encryption launcher (`extended-crypt`)  
  連携ツール `extended-crypt` を使った多重暗号化に対応
---

## 📦 Usage / 使い方

🛣️ Paths with spaces / スペースを含むパス
```bash
khurma-crypto.exe encrypt mypassword "C:\path with spaces\test.txt" encrypted.bin
```
📁 Output to a non-existent directory (auto-created)
存在しないディレクトリへの出力（自動作成）
```bash
khurma-crypto.exe encrypt mypassword test.txt "C:\new_folder\encrypted.bin"
```
🗂️ Auto-create multi-level directories
複数階層のディレクトリも自動作成
```bash
khurma-crypto.exe encrypt mypassword test.txt "C:\path\to\new\folder\encrypted.bin"
```
📄 Normal paths / 通常のパス
```bash
khurma-crypto.exe encrypt mypassword C:\path\test.txt encrypted.bin
```
🔀 Relative paths / 相対パス
```bash
khurma-crypto.exe encrypt mypassword ./test.txt ./encrypted.bin
```
💡 Example / サンプル
```bash
# Encrypt a file with a key / 暗号化
khurma-crypto.exe encrypt mySecretKey "C:\Videos\movie.mp4" "C:\Encrypted\movie_encrypted.bin"

# Decrypt the encrypted file / 復号化
khurma-crypto.exe decrypt mySecretKey "C:\Encrypted\movie_encrypted.bin" "C:\Videos\movie_restored.mp4"
```
💡Running the GUI (V1.2)
```bash
khurma-crypto.exe gui
```

## 🔁 Multi-layer Encryption / 多重暗号化

Use the companion tool `extended-crypt` to perform multi-layer encryption or decryption with multiple keys.

連携ツール `extended-crypt` を使えば、複数のキーによる多重暗号化・復号が簡単に行えます。

### 🔐 Encrypt with multiple keys / 複数キーで暗号化
```bash
extended-crypt.exe encrypt key1 key2 key3 -i test.txt -o out.bin
```
### 🔓 Decrypt in reverse order / 逆順に復号
```bash
extended-crypt.exe decrypt key3 key2 key1 -i out.bin -o restored.txt
```
### 🛠️ Specify khurma path manually / khurma-crypto.exe のパス指定
```bash
extended-crypt.exe encrypt key1 key2 -i test.txt -o out.bin --binpath "C:\tools\khurma-crypto.exe"
```

# 🧑‍💻 Quick Start for Beginners / はじめての方へ（初心者向けの使い方）

## English / 英語

This tool cannot be used by simply double-clicking with your mouse. Please follow these steps to run it from the "Command Prompt (black screen)":

### Download and Setup
1. Download `khurma-crypto.exe` from the releases page
2. Save it to an easily accessible location (e.g., `C:\Tools\khurma`)

### *💡 For Intermediate Users: Adding to PATH Environment Variable*
If you add the executable folder (e.g., C:\Tools\khurma) to your PATH environment variable, you can run khurma-crypto from any folder without typing .\khurma-crypto.exe every time.

### Opening Command Prompt from File Explorer
1. Open the folder containing `khurma-crypto.exe` in File Explorer
2. Hold **Shift** and **right-click** in an empty area of the folder
3. Select "Open PowerShell window here" or "Open Command Prompt here"

**💡 Note for Windows 11/10:** You may see "Open in Terminal" or "Open in PowerShell" - any of these options will work.

### 🚀 Command Arguments Explanation
- `encrypt`: Encrypt a file
- `decrypt`: Decrypt a file  
- `key`: Password for encryption/decryption

**File extensions are flexible!** You can use any file extension you want.

**Finding file paths:** If you're unsure about file paths, right-click the file you want to encrypt/decrypt and select "Copy as path" (Windows 11).

**Syntax:**
```bash
khurma-crypto.exe <decrypt|encrypt> <key> <input filePath> <output filePath>
```

### Example Usage

**Encrypting a file:**
To encrypt `test.txt` in the same folder:
```bash
khurma-crypto.exe encrypt mypassword test.txt encrypted.bin
```

**Decrypting back to original:**
```bash
khurma-crypto.exe decrypt mypassword encrypted.bin restored.txt
```

---

## 日本語 / Japanese

このツールは マウスでダブルクリックするだけでは使えません。以下の手順で「コマンドプロンプト（黒い画面）」から実行してください。

### ダウンロードと準備
1. リリースページ から `khurma-crypto.exe` をダウンロードします
2. わかりやすい場所（例：`C:\Tools\khurma`）に保存します

### *💡 中級者向け：環境変数PATHに追加して呼出す*

実行ファイルのフォルダ（例：C:\Tools\khurma）を環境変数 PATH に追加しておくと、
毎回 .\khurma-crypto.exe と打たずに、どのフォルダからでも khurma-crypto だけで実行できるようになります。

### エクスプローラーからコマンドプロンプトを開く
1. `khurma-crypto.exe` を置いたフォルダを エクスプローラーで開く
2. フォルダ内の何もないところで「**Shiftキーを押しながら右クリック**」→「PowerShell または コマンドプロンプトをここで開く」

**💡 Windows 11/10 では「ターミナルで開く」や「PowerShellで開く」と表示される場合がありますが、どれでもOKです。**

### 🚀 入力の引数の説明
- `encrypt`: 暗号化
- `decrypt`: 復号化
- `key`: パスワード

**ファイルの拡張子は自由です！**

**ファイルのパス指定がわからない場合は** 暗号化、復号化したいファイルを右クリックして「パスのコピー」というところを押してパスをコピーしてください。(Win11の場合)

**構文:**
```bash
khurma-crypto.exe <decrypt|encrypt> <key> <input filePath> <output filePath>
```

### 使用例

**ファイルを暗号化してみよう:**
同じフォルダにある `test.txt` を暗号化する場合：
```bash
khurma-crypto.exe encrypt パスワード test.txt encrypted.bin
```

**復号して元に戻す:**
```bash
khurma-crypto.exe decrypt パスワード encrypted.bin restored.txt
```
# ✅FAQ / よくある質問
Q. Can I use any password? / パスワードは何でもいいの？/

- Yes. We recommend using a strong password with 10+ characters. If forgotten, decryption is impossible.

英数字を混ぜた10文字以上をおすすめします。忘れると復元できません！

Q. Is the file completely hidden? / ファイルの中身は見えなくなるの？

- Yes, encrypted files are unreadable without the correct password.

完全に暗号化されるので、復号しないと中身は読み取れません。

Q. How can I run this tool from any folder / ソフトを別のフォルダから実行したい

-  Add the folder containing khurma-crypto.exe to your system PATH.

khurma-crypto.exe のパスを環境変数PATHに追加すれば、どこからでも khurma-crypto で実行できます。



## 📌 補足
- 複数階層のパスも対応しています

- 非ASCII文字（日本語ファイル名など）も対応していますが、文字コード依存の環境では注意が必要です




## ⚠️ Disclaimer / 免責事項

This tool can be freely used in commercial environments, including server integration and enterprise use.  
However, the author assumes no responsibility for any issues, damages, or losses that may occur through its usage.  
**Use at your own risk.**

本ツールは、サーバー組み込みや商用環境での利用を含め、自由にご利用いただけます。  
ただし、本ツールの使用によって生じた問題・損害・損失について、開発者は一切の責任を負いません。  
**ご利用は自己責任でお願いいたします。**


# 🙏 Special Thanks
**Built with 💙 using Rust and the awesome aes, cbc, and sha2 crates.**

Thanks for using Khurma Crypto! Stay safe and encrypt everything. 🔐

Khurma Cryptoをご利用いただきありがとうございます！安全に、すべてを暗号化してください！🔐




© 2025 khurma.lzh  
Distributed under the Apache 2.0 License.  
All other rights reserved.
