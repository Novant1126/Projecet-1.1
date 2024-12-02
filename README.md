<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Audit</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Tailwind CSS -->
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@3.3.2/dist/tailwind.min.css" rel="stylesheet">
</head>

<body class="bg-gray-100">
    <div class="container mx-auto mt-10">
        <h2 class="text-center text-2xl font-bold mb-6 text-gray-800">Form Audit Gedung dan Komponen</h2>

        <form id="auditForm" method="POST">
            <!-- Identitas Gedung -->
            <div class="card mb-4">
                <div class="card-header bg-primary text-white">Detail Tower</div>
                <div class="card-body">
                    <div class="mb-3">
                        <label for="namaGedung" class="form-label">Pilih Gedung</label>
                        <select id="namaGedung" class="form-select" name="id_gedung" required>
                            <option value="">Pilih Gedung</option>
                            <!-- Data akan dimuat dari JSON -->
                        </select>
                    </div>
                    <div class="mb-3">
                        <label for="namaTower" class="form-label">Nama Tower</label>
                        <input type="text" id="namaTower" name="nama_tower" class="form-control" required>
                    </div>
                    <div class="mb-3">
                        <label for="projectCode" class="form-label">Project Code</label>
                        <input type="text" id="projectCode" name="project_code" class="form-control" required>
                    </div>
                    <div class="mb-3">
                        <label for="PIC" class="form-label">PIC</label>
                        <input type="text" id="PIC" name="pic" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label for="jumlahLantai" class="form-label">Jumlah Lantai</label>
                        <input type="number" id="jumlahLantai" name="jumlah_lantai" class="form-control" min="1" required>
                    </div>
                </div>
            </div>
            <div class="card shadow-lg mb-5">
                <div class="card-header bg-info text-white">Audit Komponen</div>
                <div class="card-body bg-white" id="komponenContainer">
                    <!-- Komponen pertama -->
                    <div class="komponenRow border-bottom border-b border-gray-300 pb-4 mb-4">
                        <div class="row g-3">
                            <div class="col-md-6">
                                <label for="komponen" class="form-label text-gray-700">Nama Komponen</label>
                                <select class="form-select shadow-sm" name="id_komponen[]" required>
                                    <option value="">Pilih Komponen</option>
                                    <!-- Data akan dimuat dari JSON -->
                                </select>
                            </div>
                            <div class="col-md-6">
                                <label class="form-label text-gray-700">Kondisi</label>
                                <select class="form-select shadow-sm" name="kondisi[]" required>
                                    <option value="">Pilih Kondisi</option>
                                    <option value="ada">Ada</option>
                                    <option value="tidak ada">Tidak Ada</option>
                                </select>
                            </div>
                            <div class="col-md-6">
                                <label class="form-label text-gray-700">Fungsi</label>
                                <select class="form-select shadow-sm" name="fungsi[]" required>
                                    <option value="">Pilih Fungsi</option>
                                    <option value="berfungsi">Berfungsi</option>
                                    <option value="tidak berfungsi">Tidak Berfungsi</option>
                                </select>
                            </div>
                        </div>
                    </div>
                </div>
                <button type="button" class="btn btn-secondary mt-3" id="addKomponenBtn">Tambahkan Komponen</button>
            </div>

            <div class="mt-5">
                <button type="submit" class="btn btn-primary w-full mt-3 mb-5">Simpan Audit</button>
            </div>
        </form>
    </div>

    <script>
        // Muat data dari JSON
        const gedungSelect = document.getElementById('namaGedung');
        const komponenSelect = document.querySelector('select[name="id_komponen[]"]');

        fetch('data/gedung.json')
            .then(response => response.json())
            .then(data => {
                data.forEach(gedung => {
                    const option = document.createElement('option');
                    option.value = gedung.id;
                    option.textContent = gedung.nama;
                    gedungSelect.appendChild(option);
                });
            });

        fetch('data/komponen.json')
            .then(response => response.json())
            .then(data => {
                data.forEach(komponen => {
                    const option = document.createElement('option');
                    option.value = komponen.id;
                    option.textContent = komponen.nama;
                    komponenSelect.appendChild(option);
                });
            });
    </script>
</body>

</html>
