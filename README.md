[CALCUL~1.HTM](https://github.com/user-attachments/files/28060909/CALCUL.1.HTM)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Calculadora de Margem — Digital Prime</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<style>
  :root {
    --dp-laranja: #F57C20;
    --dp-laranja-escuro: #C8540F;
    --dp-laranja-medio: #E66A14;
    --dp-laranja-claro: #FF9D52;
    --dp-laranja-tint: #FFF4EC;
    --dp-dourado: #FFB955;
    --dp-branco: #FFFFFF;
    --dp-cinza-claro: #F6F4F2;
    --dp-cinza: #D9D2CB;
    --dp-cinza-texto: #6B5F55;
    --dp-texto: #2A1A0F;
    --dp-verde: #1BA864;
    --dp-vermelho: #D94B4B;
    --sombra: 0 6px 24px rgba(200, 84, 15, 0.12);
    --radius: 14px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    background: linear-gradient(135deg, var(--dp-cinza-claro) 0%, #FFEEDC 100%);
    color: var(--dp-texto);
    min-height: 100vh;
    padding: 30px 20px;
  }

  .container { max-width: 1180px; margin: 0 auto; }

  /* HEADER */
  .header {
    background: linear-gradient(135deg, var(--dp-laranja) 0%, var(--dp-laranja-escuro) 100%);
    color: var(--dp-branco);
    padding: 28px 36px;
    border-radius: var(--radius);
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: var(--sombra);
    margin-bottom: 26px;
    border-top: 4px solid var(--dp-dourado);
  }

  .logo-wrap {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .logo-circle {
    width: 56px; height: 56px;
    background: var(--dp-branco);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 800;
    color: var(--dp-laranja);
    font-size: 22px;
    letter-spacing: -1px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  }

  .brand h1 { font-size: 22px; letter-spacing: 0.5px; font-weight: 700; }
  .brand p { font-size: 13px; opacity: 0.92; margin-top: 2px; }

  .header-info {
    text-align: right;
    font-size: 13px;
    opacity: 0.95;
  }
  .header-info strong { display: block; font-size: 16px; color: var(--dp-dourado); }

  /* GRID PRINCIPAL */
  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 22px;
  }

  @media (max-width: 920px) {
    .grid { grid-template-columns: 1fr; }
  }

  .card {
    background: var(--dp-branco);
    border-radius: var(--radius);
    padding: 26px;
    box-shadow: var(--sombra);
    border: 1px solid #F1E5D8;
  }

  .card h2 {
    color: var(--dp-laranja-escuro);
    font-size: 17px;
    margin-bottom: 18px;
    padding-bottom: 12px;
    border-bottom: 2px solid var(--dp-laranja);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .card h2 .badge {
    background: var(--dp-laranja);
    color: var(--dp-branco);
    font-size: 11px;
    padding: 3px 8px;
    border-radius: 6px;
    font-weight: 600;
    letter-spacing: 0.5px;
  }

  /* UPLOAD */
  .upload-area {
    border: 2px dashed var(--dp-cinza);
    border-radius: 12px;
    padding: 32px 20px;
    text-align: center;
    transition: all 0.25s;
    cursor: pointer;
    background: var(--dp-cinza-claro);
  }
  .upload-area:hover, .upload-area.drag {
    border-color: var(--dp-laranja);
    background: var(--dp-laranja-tint);
  }
  .upload-area .icon {
    font-size: 38px;
    color: var(--dp-laranja);
    margin-bottom: 10px;
  }
  .upload-area p { color: var(--dp-cinza-texto); font-size: 14px; }
  .upload-area .small { font-size: 12px; margin-top: 5px; opacity: 0.7; }
  .upload-area input { display: none; }

  .file-info {
    margin-top: 14px;
    background: var(--dp-laranja-tint);
    border: 1px solid var(--dp-laranja-claro);
    color: var(--dp-laranja-escuro);
    padding: 10px 14px;
    border-radius: 8px;
    font-size: 13px;
    display: none;
    align-items: center;
    justify-content: space-between;
  }
  .file-info.show { display: flex; }
  .file-info button {
    background: none;
    border: none;
    color: var(--dp-vermelho);
    cursor: pointer;
    font-weight: 600;
    font-size: 13px;
  }

  .preview {
    margin-top: 16px;
    max-height: 380px;
    overflow: auto;
    border-radius: 8px;
    background: #FAFBFD;
    border: 1px solid #E0E6EE;
    display: none;
  }
  .preview.show { display: block; }
  .preview canvas, .preview img { max-width: 100%; display: block; margin: 0 auto; }

  /* FORMULÁRIO */
  .form-group { margin-bottom: 16px; }

  .form-group label {
    display: block;
    font-size: 13px;
    font-weight: 600;
    color: var(--dp-laranja-escuro);
    margin-bottom: 6px;
  }
  .form-group label .op {
    color: var(--dp-laranja);
    font-weight: 800;
    margin-right: 4px;
  }
  .form-group label .op.minus { color: var(--dp-vermelho); }

  .input-money {
    position: relative;
  }
  .input-money::before {
    content: 'R$';
    position: absolute;
    left: 14px;
    top: 50%;
    transform: translateY(-50%);
    color: var(--dp-cinza-texto);
    font-weight: 600;
    font-size: 14px;
    pointer-events: none;
  }
  .input-money input {
    width: 100%;
    padding: 12px 14px 12px 42px;
    border: 1.5px solid var(--dp-cinza);
    border-radius: 8px;
    font-size: 15px;
    color: var(--dp-texto);
    font-weight: 600;
    transition: all 0.2s;
    background: var(--dp-branco);
  }
  .input-money input:focus {
    outline: none;
    border-color: var(--dp-laranja);
    box-shadow: 0 0 0 3px rgba(245, 124, 32, 0.20);
  }

  /* RESULTADO */
  .result-card {
    background: linear-gradient(135deg, var(--dp-laranja) 0%, var(--dp-laranja-medio) 60%, var(--dp-laranja-escuro) 100%);
    color: var(--dp-branco);
    padding: 28px;
    border-radius: var(--radius);
    margin-top: 22px;
    text-align: center;
    border-top: 4px solid var(--dp-dourado);
    box-shadow: var(--sombra);
  }
  .result-card .label {
    font-size: 13px;
    text-transform: uppercase;
    letter-spacing: 2px;
    opacity: 0.95;
    margin-bottom: 8px;
  }
  .result-card .valor {
    font-size: 42px;
    font-weight: 800;
    color: var(--dp-branco);
    letter-spacing: -1px;
    text-shadow: 0 2px 8px rgba(0,0,0,0.15);
  }
  .result-card .valor.negativo { color: #FFE0E0; }
  .result-card .calc-line {
    font-size: 13px;
    opacity: 0.92;
    margin-top: 10px;
    line-height: 1.6;
  }

  /* BOTÕES */
  .btn-row {
    display: flex;
    gap: 10px;
    margin-top: 16px;
    flex-wrap: wrap;
  }
  .btn {
    padding: 11px 20px;
    border: none;
    border-radius: 8px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s;
    flex: 1;
    min-width: 130px;
  }
  .btn-primary {
    background: var(--dp-laranja);
    color: var(--dp-branco);
  }
  .btn-primary:hover { background: var(--dp-laranja-escuro); transform: translateY(-1px); }
  .btn-secondary {
    background: var(--dp-cinza-claro);
    color: var(--dp-laranja-escuro);
    border: 1.5px solid var(--dp-cinza);
  }
  .btn-secondary:hover { background: var(--dp-laranja-tint); }

  /* FOOTER */
  .footer {
    text-align: center;
    margin-top: 26px;
    font-size: 12px;
    color: var(--dp-cinza-texto);
  }
  .footer strong { color: var(--dp-laranja-escuro); }

  .alert {
    margin-top: 12px;
    padding: 10px 14px;
    border-radius: 8px;
    font-size: 13px;
    display: none;
  }
  .alert.success {
    background: #E5F8EE;
    color: #0E7A45;
    border: 1px solid #B7E5CD;
  }
  .alert.warn {
    background: #FFF6E5;
    color: #8A6500;
    border: 1px solid #F0D88E;
  }
  .alert.show { display: block; }
</style>
</head>
<body>
  <div class="container">

    <!-- HEADER -->
    <div class="header">
      <div class="logo-wrap">
        <div class="logo-circle">DP</div>
        <div class="brand">
          <h1>DIGITAL PRIME</h1>
          <p>Calculadora de Margem Consignável</p>
        </div>
      </div>
      <div class="header-info">
        <strong id="dataAtual"></strong>
        Cálculo automático de margem
      </div>
    </div>

    <div class="grid">

      <!-- COLUNA ESQUERDA: UPLOAD -->
      <div class="card">
        <h2>1. Anexar Extrato <span class="badge">PDF / IMG</span></h2>

        <label for="fileInput" class="upload-area" id="uploadArea">
          <div class="icon">📄</div>
          <p><strong>Clique aqui</strong> ou arraste o arquivo do extrato</p>
          <p class="small">Formatos aceitos: PDF, JPG, PNG</p>
          <input type="file" id="fileInput" accept=".pdf,.jpg,.jpeg,.png" />
        </label>

        <div class="file-info" id="fileInfo">
          <span id="fileName">—</span>
          <button onclick="removerArquivo()">Remover</button>
        </div>

        <div class="alert success" id="alertaLeitura">
          ✓ Valores detectados automaticamente. Confira os campos ao lado.
        </div>
        <div class="alert warn" id="alertaManual">
          ⚠ Não foi possível ler todos os valores. Preencha manualmente.
        </div>

        <div class="preview" id="preview"></div>
      </div>

      <!-- COLUNA DIREITA: FORMULÁRIO -->
      <div class="card">
        <h2>2. Valores do Extrato <span class="badge">R$</span></h2>

        <div class="form-group">
          <label><span class="op">+</span> Bruta Facult. Global</label>
          <div class="input-money">
            <input type="text" id="bruta" placeholder="0,00" oninput="formatarMoeda(this); calcular();" />
          </div>
        </div>

        <div class="form-group">
          <label><span class="op minus">−</span> Utilizada Facultativa</label>
          <div class="input-money">
            <input type="text" id="utilFacult" placeholder="0,00" oninput="formatarMoeda(this); calcular();" />
          </div>
        </div>

        <div class="form-group">
          <label><span class="op minus">−</span> Utilizada Cartão</label>
          <div class="input-money">
            <input type="text" id="utilCartao" placeholder="0,00" oninput="formatarMoeda(this); calcular();" />
          </div>
        </div>

        <div class="form-group">
          <label><span class="op minus">−</span> Utilizada Cartão Benefício</label>
          <div class="input-money">
            <input type="text" id="utilCartaoBenef" placeholder="0,00" oninput="formatarMoeda(this); calcular();" />
          </div>
        </div>

        <div class="btn-row">
          <button class="btn btn-primary" onclick="calcular()">Calcular Margem</button>
          <button class="btn btn-secondary" onclick="limparTudo()">Limpar</button>
        </div>
      </div>
    </div>

    <!-- RESULTADO -->
    <div class="result-card">
      <div class="label">Margem Atual</div>
      <div class="valor" id="resultado">R$ 0,00</div>
      <div class="calc-line" id="calcLine">Preencha os campos para calcular</div>
    </div>

    <div class="footer">
      <strong>Digital Prime</strong> © 2026 — Fórmula: Bruta Facult. Global − Utilizada Facultativa − Utilizada Cartão − Utilizada Cartão Benefício
    </div>
  </div>

<script>
  pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

  // Data atual
  const dataAtual = new Date().toLocaleDateString('pt-BR', { day: '2-digit', month: 'long', year: 'numeric' });
  document.getElementById('dataAtual').textContent = dataAtual;

  // FORMATAÇÃO MONETÁRIA
  function formatarMoeda(input) {
    let v = input.value.replace(/\D/g, '');
    if (!v) { input.value = ''; return; }
    v = (parseInt(v) / 100).toFixed(2);
    v = v.replace('.', ',');
    v = v.replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.');
    input.value = v;
  }

  function parseValor(str) {
    if (!str) return 0;
    return parseFloat(String(str).replace(/\./g, '').replace(',', '.')) || 0;
  }

  function formatarReal(num) {
    return num.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
  }

  // CÁLCULO PRINCIPAL
  function calcular() {
    const bruta = parseValor(document.getElementById('bruta').value);
    const uf = parseValor(document.getElementById('utilFacult').value);
    const uc = parseValor(document.getElementById('utilCartao').value);
    const ucb = parseValor(document.getElementById('utilCartaoBenef').value);

    const margem = bruta - uf - uc - ucb;

    const resEl = document.getElementById('resultado');
    resEl.textContent = formatarReal(margem);
    resEl.classList.toggle('negativo', margem < 0);

    if (bruta === 0 && uf === 0 && uc === 0 && ucb === 0) {
      document.getElementById('calcLine').textContent = 'Preencha os campos para calcular';
    } else {
      document.getElementById('calcLine').innerHTML =
        `${formatarReal(bruta)} − ${formatarReal(uf)} − ${formatarReal(uc)} − ${formatarReal(ucb)} = <strong>${formatarReal(margem)}</strong>`;
    }
  }

  // LIMPAR
  function limparTudo() {
    ['bruta','utilFacult','utilCartao','utilCartaoBenef'].forEach(id => document.getElementById(id).value = '');
    calcular();
    removerArquivo();
  }

  // UPLOAD
  const uploadArea = document.getElementById('uploadArea');
  const fileInput = document.getElementById('fileInput');
  const fileInfo = document.getElementById('fileInfo');
  const preview = document.getElementById('preview');

  ['dragenter','dragover'].forEach(ev => {
    uploadArea.addEventListener(ev, e => { e.preventDefault(); uploadArea.classList.add('drag'); });
  });
  ['dragleave','drop'].forEach(ev => {
    uploadArea.addEventListener(ev, e => { e.preventDefault(); uploadArea.classList.remove('drag'); });
  });
  uploadArea.addEventListener('drop', e => {
    if (e.dataTransfer.files.length) {
      fileInput.files = e.dataTransfer.files;
      processarArquivo(e.dataTransfer.files[0]);
    }
  });
  fileInput.addEventListener('change', e => {
    if (e.target.files.length) processarArquivo(e.target.files[0]);
  });

  function removerArquivo() {
    fileInput.value = '';
    fileInfo.classList.remove('show');
    preview.classList.remove('show');
    preview.innerHTML = '';
    document.getElementById('alertaLeitura').classList.remove('show');
    document.getElementById('alertaManual').classList.remove('show');
  }

  async function processarArquivo(file) {
    document.getElementById('fileName').textContent = file.name;
    fileInfo.classList.add('show');
    preview.innerHTML = '';
    document.getElementById('alertaLeitura').classList.remove('show');
    document.getElementById('alertaManual').classList.remove('show');

    if (file.type === 'application/pdf') {
      await processarPDF(file);
    } else if (file.type.startsWith('image/')) {
      processarImagem(file);
      document.getElementById('alertaManual').classList.add('show');
    }
  }

  function processarImagem(file) {
    const reader = new FileReader();
    reader.onload = e => {
      preview.innerHTML = `<img src="${e.target.result}" alt="Extrato" />`;
      preview.classList.add('show');
    };
    reader.readAsDataURL(file);
  }

  async function processarPDF(file) {
    try {
      const arrayBuffer = await file.arrayBuffer();
      const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
      const page = await pdf.getPage(1);

      // Renderiza preview visual
      const viewport = page.getViewport({ scale: 1.2 });
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');
      canvas.width = viewport.width;
      canvas.height = viewport.height;
      await page.render({ canvasContext: ctx, viewport }).promise;
      preview.appendChild(canvas);
      preview.classList.add('show');

      // Extrai itens de texto com posições (x, y) de todas as páginas
      const itens = [];
      for (let i = 1; i <= pdf.numPages; i++) {
        const p = await pdf.getPage(i);
        const content = await p.getTextContent();
        content.items.forEach(it => {
          const s = it.str;
          if (!s || !s.trim()) return;
          itens.push({
            str: s,
            x: it.transform[4],
            y: it.transform[5], // em pdf.js, y maior = mais ao topo
            width: it.width || 0
          });
        });
      }

      detectarValoresPosicional(itens);
    } catch (err) {
      console.error('Erro ao ler PDF:', err);
      document.getElementById('alertaManual').classList.add('show');
    }
  }

  // ====== DETECÇÃO POR LINHAS DE VALORES ======
  // Estratégia: identificar a LINHA com mais R$ (linha Bruta/Líquida = ~8 valores)
  // e a linha com 3 R$ (linha Utilizada), depois usar índices fixos dentro de cada linha.
  // Funciona porque, no extrato, as colunas seguem ordem previsível da esquerda para a direita.
  function detectarValoresPosicional(itens) {
    // 1. Determina o limite do cabeçalho (antes do "Demonstrativo")
    const itemDemo = itens.find(i => /demonstrativo/i.test(i.str));
    const yLimite = itemDemo ? itemDemo.y : -Infinity;

    // 2. Coleta todos os valores R$ X,XX que estão NA ÁREA do cabeçalho
    const tolY = 5;
    const valoresPos = [];
    for (let i = 0; i < itens.length; i++) {
      if (itens[i].y < yLimite) continue;
      const s = itens[i].str.trim();

      // Caso 1: item contém "R$ X,XX" completo
      const mFull = s.match(/R\$\s*([\d\.]+,\d{2})/);
      if (mFull) {
        valoresPos.push({ valor: mFull[1], x: itens[i].x, y: itens[i].y });
        continue;
      }
      // Caso 2: item é "R$" sozinho, seguido por outro item com o número
      if (s === 'R$' && i + 1 < itens.length) {
        const next = itens[i+1].str.trim();
        if (/^[\d\.]+,\d{2}$/.test(next) && Math.abs(itens[i+1].y - itens[i].y) < tolY) {
          valoresPos.push({ valor: next, x: itens[i].x, y: itens[i].y });
        }
      }
    }

    // 3. Agrupa valores por linha (y próximo)
    const linhasV = [];
    for (const v of valoresPos) {
      let linha = linhasV.find(l => Math.abs(l.y - v.y) < tolY);
      if (!linha) {
        linha = { y: v.y, valores: [] };
        linhasV.push(linha);
      }
      linha.valores.push(v);
    }
    linhasV.forEach(l => l.valores.sort((a, b) => a.x - b.x));
    linhasV.sort((a, b) => b.y - a.y); // de cima para baixo

    // 4. Identifica a linha Bruta/Líquida (a com mais valores R$, tipicamente 6-8)
    let linhaBrutaLiquida = null;
    for (const l of linhasV) {
      if (!linhaBrutaLiquida || l.valores.length > linhaBrutaLiquida.valores.length) {
        linhaBrutaLiquida = l;
      }
    }

    // 5. Identifica a linha Utilizada (a com 3 valores, geralmente abaixo da Bruta/Líquida)
    //    Preferimos a linha com EXATAMENTE 3 valores e y menor que a linha Bruta/Líquida
    let linhaUtilizada = null;
    for (const l of linhasV) {
      if (l === linhaBrutaLiquida) continue;
      if (l.valores.length === 3) {
        if (!linhaUtilizada || (linhaBrutaLiquida && l.y < linhaBrutaLiquida.y && (!linhaUtilizada || linhaUtilizada.y > l.y))) {
          linhaUtilizada = l;
        } else if (!linhaUtilizada) {
          linhaUtilizada = l;
        }
      }
    }
    // Fallback: qualquer linha com >=3 valores diferente da Bruta/Líquida
    if (!linhaUtilizada) {
      linhaUtilizada = linhasV.find(l => l !== linhaBrutaLiquida && l.valores.length >= 3);
    }

    let achou = 0;

    // 6. Mapeia índices fixos:
    //    Linha Bruta/Líquida (8 col): [Bruta Comp | Líq Comp | Bruta FG | Líq FG | Bruta C | Líq C | Bruta CB | Líq CB]
    //    Posição 2 (0-indexed) = Bruta Facult. Global
    if (linhaBrutaLiquida && linhaBrutaLiquida.valores.length >= 3) {
      document.getElementById('bruta').value = linhaBrutaLiquida.valores[2].valor;
      achou++;
    }

    //    Linha Utilizada (3 col): [Utilizada Facult | Utilizada Cartão | Utilizada Cartão Benefício]
    if (linhaUtilizada && linhaUtilizada.valores.length >= 3) {
      document.getElementById('utilFacult').value = linhaUtilizada.valores[0].valor;
      document.getElementById('utilCartao').value = linhaUtilizada.valores[1].valor;
      document.getElementById('utilCartaoBenef').value = linhaUtilizada.valores[2].valor;
      achou += 3;
    }

    if (achou >= 4) {
      document.getElementById('alertaLeitura').classList.add('show');
    } else {
      document.getElementById('alertaManual').classList.add('show');
    }
    calcular();
  }
</script>
</body>
</html>
