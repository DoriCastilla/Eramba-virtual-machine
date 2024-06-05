<button id="boton" onclick="copiar()" value="otra pueba">Copiar texto</button>
<input type="text" value="Lorem ipsum dolor site amet" id="target1" readonly>
<br>
<label>Texto copiado (Ctrl + V)</label>
<input type="text" id="target2">
<br>
* {
  margin:5px;
  padding:5px;
  border-radius:5px;
}
function copiar(){
  var origen = document.getElementById('target1');
  var destino = document.getElementById('target2');
  var copyFrom = document.createElement("textarea");
  copyFrom.textContent = origen.value;
  var body = document.getElementsByTagName('body')[0];
  body.appendChild(copyFrom);
  copyFrom.select();
  document.execCommand('copy');
  body.removeChild(copyFrom);
  destino.focus();
  document.execCommand('paste');
}
