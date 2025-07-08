#  Khurma Crypto

**Secure and blazing-fast AES-256 file encryption tool for all file types, powered by Rust.**  
**あらゆるファイル形式に対応した、高速かつ安全なAES-256ファイル暗号化ツール（Rust製）です。**

# Binary Format Support / 対応フォーマット
This tool treats all files as binary (Vec<u8>), so it supports:
このツールはすべてのファイルをバイナリとして扱うため、以下に対応しています：

**Support format**
Any other format / その他すべての形式


## Use Cases / 主な用途

- **Safely storing files locally**  
  ローカルに安全にファイルを保存したいとき

- **Encrypting files for secure transfer or sharing**  
  暗号化してファイルを転送・共有したいとき

- **Protecting data in offline environments or on USB drives**  
  オフライン環境やUSBメモリでの情報保護

This tool helps you keep your important files completely secure.  
あなたの大切なファイルをしっかり守ります。

---

##  Features / 特徴

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

---

## 📦 Usage / 使い方

```bash
# Encrypt a file / ファイルを暗号化
khurma-crypto encrypt <seed> <input_file> <output_file>

# Decrypt a file / ファイルを復号化
khurma-crypto decrypt <seed> <input_file> <output_file>
```

# 🙏 Special Thanks
**Built with 💙 using Rust and the awesome aes, cbc, and sha2 crates.**


This tool can be freely used in commercial environments, including server integration and enterprise use.  
However, the author assumes no responsibility for any issues, damages, or losses that may occur through its usage.  
**Use at your own risk.**

本ツールは、サーバー組み込みや商用環境での利用を含め、自由にご利用いただけます。  
ただし、本ツールの使用によって生じた問題・損害・損失について、開発者は一切の責任を負いません。  
**ご利用は自己責任でお願いいたします。**
