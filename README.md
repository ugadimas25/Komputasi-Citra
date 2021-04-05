# Komputasi-Citra
Script untuk melakukan komputasi citra dengan menggunakan data elevasi
```javascript

// 03 KOMPUTASI CITRA

// Cari 'dsm' (model permukaan digital) dan temukan:
var dsm = ee.Image('JAXA/ALOS/AW3D30_V1_1');

// Dapatkan ketinggian dalam pita saluran meter.
var elev = dsm.select('AVE');

// Perhitungan ini ('junk') hanyalah contoh matematika dengan citra.
var junk = elev.add(3);
Map.addLayer(junk, {min: 0, max: 500}, 'junk');

// Operasi relasional pada citra. Temukan semua tempat
// ketinggian lebih dari 500 meter. Citra biner.
var elevGt500 = elev.gt(500);
// Ini adalah trik yang berguna. Setel semua nol piksel menjadi 'no data' (masked).
elevGt500 = elevGt500.updateMask(elevGt500);
Map.addLayer(elevGt500, {palette: ['yellow']}, 'elevGt500');

// Gunakan metode statis untuk perhitungan yang lebih kompleks.
var terrain = ee.Terrain.products(elev);
// Cetak untuk mengetahui band apa yang ada di sana.
print('terrain', terrain);
Map.addLayer(terrain, {bands: ['hillshade']}, 'hillshade');
