# Bingöl Isı-Sağlık Erken Uyarı Sistemi

Bingöl ilinde yerleşim ölçeğinde ısı-sağlık kırılganlığını haritalayan ve
günlük sıcaklık tahminini yerel eşiklerle karşılaştıran açık bir web
uygulaması.

## Ne yapıyor

- **Isı fazlası.** Landsat 8/9 yaz yüzey sıcaklığından rakımın etkisi
  ayrılarak her yerleşimin kendi ısınması hesaplanır (100 metrede 0,52 °C).
- **Kırılganlık endeksi.** Maruziyet, hassasiyet ve uyum kapasitesi
  eksikliği IPCC çerçevesinde, ikili karşılaştırmayla (AHP, tutarlılık
  oranı < 0,01) ağırlıklandırılır.
- **Model ve senaryo.** XGBoost, 600 metrelik uzamsal bloklarla
  doğrulanır (R² = 0,580 ± 0,024). Yeşillendirme senaryosu NDVI +0,15
  varsayımıyla hesaplanır.
- **Günlük uyarı.** Open-Meteo tahmini, her yerleşimin kendi eşiğiyle
  karşılaştırılır.

## Çalıştırma

Statik bir sitedir, derleme gerektirmez. Yerelde açmak için klasörde:

    python -m http.server 8000

ardından <http://localhost:8000> adresine gidin. (Tarayıcıda dosyayı
doğrudan açmak GeoJSON okumasını engeller; basit bir sunucu gerekir.)

## Klasör yapısı

    index.html          uygulamanın tamamı (HTML + CSS + JS)
    data/
      *.geojson         il sınırı, ilçe, mahalle, yerleşim, müdahale alanı
      katman_*.png      analiz katmanlarının görüntüleri
      katmanlar.json    katman tanımları ve renk ölçekleri
      esikler.json      yerleşim bazlı sıcaklık eşikleri
      grafik/           model ve senaryo grafikleri (açık ve koyu tema)

## Veri kaynakları

Landsat 8/9 Collection 2 Level 2 · ESA WorldCover v200 · Esri Yıllık Arazi
Örtüsü · JRC GHSL · Copernicus DEM GLO-30 · WorldPop 2025 · TÜİK ADNKS ·
Open-Meteo

Kullanılan verilerin tamamı ücretsiz ve küresel ölçekte erişilebilirdir;
yöntem Türkiye'nin her ili için yinelenebilir.

## Kullanılan araçlar

Google Earth Engine · ArcGIS Pro · Python (arcpy, NumPy, XGBoost, SHAP,
Matplotlib) · Leaflet
