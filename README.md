# pertemuan-15


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Per 15</title>
    <link rel="stylesheet" href="css/bootstrap.css">
    <style type="text/css">
        .sptombol{
            padding-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="row">

            <div class="col-4">
                <form action="" name="frminput">
                    <label for="NIM">NIM:</label>
                    <input type="text" class="form-control" id="txNIM">
                    
                    <label for="kelas">kelas:</label>
                    <input type="text" class="form-control" id="txKLS">

                    <label for="IDMK">kode matakuliah</label>
                    <input type="text" class="form-control" id="txIDMK">

                    <div class="form-group sptombol">
                        <button type="button" class="btn btn-primary" id="cmdcari">cari data</button>
                    </div>
                </form>

            </div>

            <div class="col-4">
                <h3>Data Nilai</h3>
                <div id="lbNIM">
                    NIM:
                    <span id="vtxNIM">
                        9999999999
                    </span>
                </div>
                <div id="lbnama">
                    Nama
                    <span id="vtxNAMA">
                        : NAMA MAHASISWA
                    </span>
                </div>
                <div>
                    <h3>DATA NILAI</h3>
                    <div id="vnilai"></div>
                </div>
            </div>
            <div class="col-4">
                <div>
                    <h3>DATA KEHADIRAN</h3>
                    <div id="vhadir"></div>
                </div>
            </div>

        </div>
    </div>
</body>
<script src="js/bootstrap.js"></script>
<script type="text/javascript" src="jquery.min.js"></script>
<script type="text/javascript">
    $(document).ready(function(){

        $("#cmdcari").click(function(){
            var nim = $("#txNIM").val();
            var kls = $("#txKLS").val();
            var idmk = $("#txIDMK").val();
            var prm = "getpress-"+idmk+"-"+nim+"-"+kls+".html";
            $.ajax({
                type: "GET",
                url: "https://mhstiki.artha.web.id/api/"+prm,
                dataType: "json",
                success: function(data){
                    var vnim = ": "+data["NIM"];
                    var vnama = ": "+data["NAMA"];
                    $("#vtxNIM").html(vnim);
                    $("#vtxNAMA").html(vnama);
                    /*list Nilai*/
                    var nnilai = "<ol><ul>Nilai Aktif: "+data["N_AKTIF"]+"</ul><ul>Nilai Tugas: "+data["N_TUGAS"]+"</ul><ul>Nilai QUIS: "+data["N_QUIS"]+"</ul><ul>Nilai UTS: "+data["N_UTS"]+"</ul><ul>Nilai UAS: "+data["N_UAS"]+"</ul><ul>Nilai Akhir: "+data["N_NA"]+"</ul><ul>Grade: "+data["GRADE"]+"</ol>";
                    $("#vnilai").html(nnilai);
                    /*list hadir*/
                    var jmlpertemuan = 16;
                    var jhadir = jmlpertemuan - parseInt(data["MANGKIR"]);
                    var hadir = "<h3>Presensi</h3>Jumlah Tidak Kehadiran: "+data["MANGKIR"]+"("+data["PROS_HADIR"]+")";
                    $("#vhadir").html(hadir);
                }
            });
        });
    });
</script>
</html>
