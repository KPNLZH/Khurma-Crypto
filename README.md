# 📦 Khurma-Crypto DLL
このライブラリは、Rustで実装されたAES256暗号化アルゴリズムを多言語から利用するためのものです。メモリ管理に特に注意して設計されています。

## 関数一覧 📝
`encrypt_data` 🔒
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

#### 注意: この関数は、ポインタが指すデータの内容には関知しません。Rustのメモリ管理システムに所有権を戻すため、正しいポインタとサイズを渡す必要があります。

## 2. 使い方 🛠️
`encrypt_data` または `decrypt_data` を呼び出してデータを取得します。

取得したデータポインタをC言語側で使用します。

#### データが不要になったら、必ず free_crypto_data を呼び出してメモリを解放してください。
