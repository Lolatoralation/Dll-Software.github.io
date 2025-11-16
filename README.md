<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>RepairDLL – Modern App</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; font-family: "Segoe UI", sans-serif; }
html, body { width: 100vw; height: 100vh; overflow: hidden; background: #0d0f14; }

.app { display: flex; width: 100%; height: 100%; }

.sidebar { width: 260px; height: 100%; background: rgba(255,255,255,0.05); backdrop-filter: blur(20px); padding: 25px 15px; display: flex; flex-direction: column; gap: 20px; border-right: 1px solid rgba(255,255,255,0.1); }
.sidebar h1 { color: white; font-size: 22px; text-align: center; margin-bottom: 15px; }
.tab { padding: 12px 18px; border-radius: 12px; color: white; background: rgba(255,255,255,0.04); cursor: pointer; transition: 0.25s; font-size: 15px; }
.tab:hover { background: rgba(255,255,255,0.12); }
.tab.active { background: #4f9cff; color: black; font-weight: 600; }

.content { flex: 1; height: 100%; padding: 40px; overflow-y: auto; color: white; display: flex; justify-content: center; align-items: center; }

.card { width: 70%; max-width: 800px; background: rgba(255,255,255,0.07); backdrop-filter: blur(25px); padding: 40px; border-radius: 22px; border: 1px solid rgba(255,255,255,0.15); box-shadow: 0 0 25px rgba(0,0,0,0.25); animation: fadeIn 0.5s ease; }
@keyframes fadeIn { from { opacity: 0; transform: scale(0.97);} to { opacity: 1; transform: scale(1);} }
.card h2 { text-align: center; margin-bottom: 25px; font-size: 26px; }

.drop-area { width: 100%; height: 220px; background: rgba(255,255,255,0.06); border: 3px dashed rgba(255,255,255,0.25); border-radius: 20px; display: flex; justify-content: center; align-items: center; color: #d9d9d9; font-size: 18px; margin-bottom: 30px; transition: 0.25s; white-space: pre-line; text-align: center; }
.drop-area.dragover { background: rgba(79,156,255,0.15); border-color: #4f9cff; color: white; }

.buttons { display: flex; width: 100%; justify-content: space-between; }
.btn { width: 48%; padding: 14px; font-size: 16px; border: none; border-radius: 14px; cursor: pointer; transition: 0.25s; }
.btn:hover { transform: scale(1.03); }
.repair { background: #4f9cff; color: black; }
.reset { background: rgba(255,255,255,0.18); color: white; }

.smalltext { margin-top: 25px; font-size: 14px; text-align: center; color: #bcbcbc; }

.fullscreen-btn { position: fixed; right: 20px; top: 15px; padding: 10px 16px; background: rgba(255,255,255,0.1); color: white; border-radius: 12px; border: 1px solid rgba(255,255,255,0.2); cursor: pointer; backdrop-filter: blur(10px); transition: 0.25s; }
.fullscreen-btn:hover { background: rgba(255,255,255,0.25); }
</style>
</head>
<body>
<button class="fullscreen-btn" onclick="toggleFullscreen()">⛶ Pantalla completa</button>

<div class="app">
  <div class="sidebar">
    <h1>RepairDLL</h1>
    <div class="tab active"> Reparar DLL </div>
    <div class="tab"> Descargas </div>
    <div class="tab"> Información </div>
  </div>

  <div class="content" id="content">
    <div class="card">
      <h2>Reparador de DLL</h2>
      <div class="drop-area" id="dropArea">Arrastra aquí tu archivo DLL</div>

      <div class="buttons">
        <button class="btn repair">Reparar DLL</button>
        <button class="btn reset">Restablecer DLL</button>
      </div>

      <div class="smalltext">Los archivos de bloc de notas no son compatibles con el sistema, necesita volverlos a descargar.</div>
    </div>
  </div>
</div>

<script>
function toggleFullscreen() {
  if (!document.fullscreenElement) document.documentElement.requestFullscreen();
  else document.exitFullscreen();
}

const dropArea = document.getElementById("dropArea");

dropArea.addEventListener("dragover", e => { e.preventDefault(); dropArea.classList.add("dragover"); });
dropArea.addEventListener("dragleave", () => dropArea.classList.remove("dragover"));
dropArea.addEventListener("drop", e => {
  e.preventDefault(); dropArea.classList.remove("dragover");
  const file = e.dataTransfer.files[0];
  if (!file) return;
  if (!file.name.endsWith(".dll")) { dropArea.textContent = "Archivo incompatible. Solo DLL."; return; }
  dropArea.textContent = `Archivo detectado:\n${file.name}\nTamaño: ${(file.size/1024).toFixed(1)} KB`;
});
</script>
</body>
</html>
