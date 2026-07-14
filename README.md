# RabbitMQ Tabanlı secp256k1 İmzalama ve Doğrulama Servisi

Bu proje, Bouncy Castle kullanarak secp256k1 eğrisi üzerinde ECDSA imzalama ve imza doğrulama işlemlerini RabbitMQ üzerinden asenkron olarak gerçekleştiren bir Java servisidir. İmza formatı DER olarak kullanılmıştır.

## Güvenlik Uyarısı (ÖNEMLİ)
⚠️ Private key'in dosyada tutulması yalnızca geliştirme ve test amacıyla yapılmıştır. Production (Canlı) ortam için bu yaklaşım kesinlikle güvenli kabul edilmemelidir ve uygun değildir!

## Kurulum
Projeyi derlemek için:
mvn clean package

RabbitMQ broker'ı Docker üzerinden ayağa kaldırmak için:
docker compose up -d

## Çalıştırma Modları
Keygen Modu (Anahtar Üretimi):
./scripts/run-keygen.sh

Signer Modu (İmzalama Servisi):
./scripts/run-signer.sh

Verifier Modu (Doğrulama Servisi):
./scripts/run-verifier.sh

## Benchmark Test Komutları
Sign (İmzalama) Yük Testi (10.000 mesaj):
./scripts/run-benchmark-sign.sh

Verify (Doğrulama) Yük Testi (10.000 mesaj):
./scripts/run-benchmark-verify.sh

## Örnek Benchmark Çıktıları

Aşağıda yer alan test sonuçları, lokal ortamda 10.000 mesajlık yük testi (benchmark-client) çalıştırılarak elde edilmiştir.

### Sign (İmzalama) Benchmark Sonucu
Operation: sign
Message count: 10000
Success: 10000
Error: 0
Average latency: 5 ms
P95 latency: 5 ms
P99 latency: 6 ms
Throughput: 879,43 req/sec
Total duration: 11,37 sec

### Verify (Doğrulama) Benchmark Sonucu
Operation: verify
Message count: 10000
Success: 10000
Error: 0
Average latency: 5 ms
P95 latency: 5 ms
P99 latency: 6 ms
Throughput: 1063,60 req/sec
Total duration: 9,40 sec

## Kriptografik Standartlar
- İmza Formatı: DER (Distinguished Encoding Rules)
- Public Key Formatı: X.509 SubjectPublicKeyInfo formatında dışa aktarılmaktadır.
