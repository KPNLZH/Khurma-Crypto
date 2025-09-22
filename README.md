# 📦 Khurma-Crypto DLL
このライブラリは、Rustで実装されたAES256暗号化アルゴリズムを多言語から利用するためのものです。メモリ管理に特に注意して設計されています。

## 関数一覧 📝
`encrypt_data` 🔒
`decrypt_data` 🔒
`free_crypto_data` 🗑️
メモリ上の生データをAES256で暗号化します。

## C関数シグネチャ
`uint8_t* encrypt_data(const uint8_t* data_ptr, size_t data_len, const char* seed_ptr, size_t* output_len);`

## パラメータ

`data_ptr`: 暗号化したい生データへのポインタ。

`data_len`: 入力データのバイト数。

`seed_ptr`: 暗号化/復号化のキーとIVを生成するための文字列ポインタ。

`output_len`: 暗号化されたデータのバイト数を出力するためのポインタ。呼び出し元で確保しておく必要があります。

## 戻り値

暗号化されたデータへのポインタ。

#### 重要: このポインタはヒープメモリを指しており、使用後は必ず free_crypto_data 関数で解放する必要があります。

`decrypt_data` 🔑
メモリ上の暗号化されたデータを復号化します。

C関数シグネチャ
`uint8_t* decrypt_data(const uint8_t* data_ptr, size_t data_len, const char* seed_ptr, size_t* output_len);`

## パラメータ

`data_ptr`: 復号化したい暗号化済みデータへのポインタ。

`data_len`: 入力データのバイト数。

`seed_ptr`: 暗号化/復号化のキーとIVを生成するための文字列ポインタ。

`output_len`: 復号化されたデータのバイト数を出力するためのポインタ。呼び出し元で確保しておく必要があります。

## 戻り値

復号化されたデータへのポインタ。

#### 重要: このポインタはヒープメモリを指しており、使用後は必ず free_crypto_data 関数で解放する必要があります。

`free_crypto_data` 🗑️
`encrypt_data`または`decrypt_data`が返したヒープメモリを安全に解放します。

## C関数シグネチャ
`void free_crypto_data(uint8_t* data_ptr, size_t data_len);`

## パラメータ

`data_ptr`: 解放したいデータへのポインタ。

`data_len`: 解放したいデータのバイト数。

##### 注意: この関数は、ポインタが指すデータの内容には関知しません。Rustのメモリ管理システムに所有権を戻すため、正しいポインタとサイズを渡す必要があります。

## 2.EXE版との互換性について 🤝

このDLL版のライブラリは、単体で動作するコマンドラインツール（EXE版）と同じコアアルゴリズムを使用しています。

#### パイプ（Pipe）モードでの連携 🚀
コマンドラインツールは、パイプモードをサポートしており、標準入力からデータを受け取り、暗号化または復号化を実行して、結果を標準出力に出力します。

詳しい説明はCLI版のドキュメントをご覧ください

**これにより、C言語やPythonなどのプログラムから、このライブラリを直接呼び出す代わりに、EXE版をパイプで実行してデータのやり取りを行うことも可能です。**

#### この柔軟性は、既存のシステムに組み込む際に非常に役立ちます。

## 3. 使い方 🛠️
`encrypt_data` または `decrypt_data` を呼び出してデータを取得します。

取得したデータポインタをC言語側で使用します。

#### データが不要になったら、必ず free_crypto_data を呼び出してメモリを解放してください。

### テスト用サンプルコード 💾
```Python
import ctypes

# DLLをロードする
try:
    lib = ctypes.CDLL("./khurma_crypto.dll")
except OSError as e:
    print(f"DLLのロード中にエラーが発生しました: {e}")
    print("DLLファイルが正しいパスに存在するか確認してな！")
    exit()

# encrypt_data関数の型定義 (変更なし)
lib.encrypt_data.argtypes = (ctypes.POINTER(ctypes.c_ubyte), ctypes.c_size_t, ctypes.c_char_p, ctypes.POINTER(ctypes.c_size_t))
lib.encrypt_data.restype = ctypes.POINTER(ctypes.c_ubyte)

# decrypt_data関数の型定義を追加
lib.decrypt_data.argtypes = (ctypes.POINTER(ctypes.c_ubyte), ctypes.c_size_t, ctypes.c_char_p, ctypes.POINTER(ctypes.c_size_t))
lib.decrypt_data.restype = ctypes.POINTER(ctypes.c_ubyte)

# free_crypto_data関数の型定義 (変更なし)
lib.free_crypto_data.argtypes = (ctypes.POINTER(ctypes.c_ubyte), ctypes.c_size_t)
lib.free_crypto_data.restype = None

def test_encryption_and_decryption():
    print("----- 暗号化と復号化のテスト開始 -----")
    
    # 元のデータとシード（鍵）を準備
    original_data = b"Hello, this is a test string to be encrypted and decrypted using Python and Rust!"
    seed = "anothersecretpassword456"

    # 暗号化するデータをc_ubyteの配列に変換
    data_array = (ctypes.c_ubyte * len(original_data))(*original_data)
    
    # === 暗号化処理 ===
    print("\n--- 暗号化 ---")
    enc_output_len = ctypes.c_size_t(0)
    encrypted_ptr = lib.encrypt_data(
        data_array,
        len(original_data),
        seed.encode('utf-8'),
        ctypes.byref(enc_output_len)
    )

    if not encrypted_ptr:
        print("エラー: 暗号化に失敗しました。")
        return
    
    encrypted_data = ctypes.string_at(encrypted_ptr, enc_output_len.value)
    
    print(f"元のデータ: {original_data.decode('utf-8')}")
    print(f"暗号化されたデータのサイズ: {enc_output_len.value} バイト")
    print(f"暗号化されたデータ（一部）: {encrypted_data[:20].hex()}...")
    
    # === 復号化処理 ===
    print("\n--- 復号化 ---")
    dec_output_len = ctypes.c_size_t(0)
    
    # 暗号化されたデータをc_ubyteの配列に変換
    enc_data_array = (ctypes.c_ubyte * len(encrypted_data))(*encrypted_data)
    
    decrypted_ptr = lib.decrypt_data(
        enc_data_array,
        len(encrypted_data),
        seed.encode('utf-8'),
        ctypes.byref(dec_output_len)
    )
    
    # 復号化後のメモリを解放する前に、暗号化後のメモリを解放
    lib.free_crypto_data(encrypted_ptr, enc_output_len.value)

    if not decrypted_ptr:
        print("エラー: 復号化に失敗しました。")
        return

    decrypted_data = ctypes.string_at(decrypted_ptr, dec_output_len.value)
    
    print(f"復号化されたデータのサイズ: {dec_output_len.value} バイト")
    print(f"復号化されたデータ: {decrypted_data.decode('utf-8')}")
    
    # 元のデータと一致するか確認
    if original_data == decrypted_data:
        print("\n✅ テスト成功！元のデータと復号化されたデータは一致しました。")
    else:
        print("\n❌ テスト失敗！データが一致しません。")

    # 復号化後のメモリを解放
    lib.free_crypto_data(decrypted_ptr, dec_output_len.value)
    
    print("\n----- テスト完了 -----")

# テストを実行！
if __name__ == "__main__":
    test_encryption_and_decryption()
```

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


