# WAN Speed Logger — instaladores

Este repositório guarda apenas os instaladores do **WAN Speed Logger**, uma aplicação para Windows 11
que mede periodicamente a velocidade da ligação à internet, testa a rede local e compara servidores DNS.
O código-fonte não é público.

## Instalar
Abra [Releases](../../releases/latest), descarregue `WAN-Speed-Logger-Setup-<versão>.exe` e execute-o.

O instalador não tem assinatura digital, por isso o Windows pode mostrar o aviso «O Windows protegeu o PC».
Nesse caso, clique em **Mais informações → Executar mesmo assim**.

## Atualizações
A partir da versão 2.5.0 a aplicação procura novas versões neste repositório e avisa quando há uma
atualização; basta carregar em **Atualizar agora**. As definições e o histórico são mantidos.

## 🚀 Principais Funcionalidades

### 🌐 Testes à Internet (WAN)
* **Fornecedores Suportados:**
  * **M-Lab NDT7** *(padrão)*: Servidores mais próximos via Locate API (dados abertos e anonimizados).
  * **LibreSpeed**: Suporte a servidores públicos ou instância própria/privada.
  * **Speedtest by Ookla**: Integração com a CLI oficial (`winget install Ookla.Speedtest.CLI`). Cache local de servidores (`ookla-servers.json`) para prevenir erros de limite (HTTP 429) e suporte a ID manual.
* **Perfis de Duração:** Leve (5s), Normal (10s) e Completo (20s) por sentido *(sujeito a limites de protocolo do fornecedor)*.
* **Agendamento Inteligente:**
  * Intervalo configurável entre 1 e 1440 minutos, com opção de pausa e teste imediato (*Testar agora*).
  * **Deteção de ecrã inteiro:** Adia automaticamente testes agendados se detetar jogos (incluindo *borderless windowed*), vídeos ou apresentações ativas.
* **Análise de Contrato:** Comparação em tempo real com a largura de banda contratada e alertas de velocidade abaixo do limite aceitável.

### 🏠 Rede Interna (LAN Benchmark)
* **Diagnóstico Local:** Mede largura de banda, ping e jitter entre o PC e outros dispositivos (smartphones, tablets, PCs) na mesma rede.
* **Sem Instalação no Cliente:** Inicia um servidor HTTP local seguro (porta padrão `8090`) com interface web dedicada via QR Code ou endereço direto.
* **Telemetria Completa:** Regista tipo de dispositivo remoto e estado da interface local (Wi-Fi/Ethernet, SSID, banda, sinal e velocidade de sincronização).
* **Gestão de Sessão:** Encerramento automático após 30 min de inatividade ou modo contínuo em segundo plano.

### ⚡ Benchmark de DNS
* **Comparação em Tempo Real:** Avalia 14 resolvers DNS públicos (incluindo DNS4EU, Cloudflare, Google, SafeDNS, etc.).
* **Protocolos:** Comparações lado a lado entre DNS Clássico (UDP 53) e DNS Seguro (DoH).
* **Métricas:** Resoluções em paralelo com e sem cache, tempos de resposta (mediana/mín/máx), ping e taxa de erro.
* **Deteção de Interceção:** Identifica se os pedidos estão a ser manipulados por firewalls, routers, antivírus ou proxies/VPN locais.
* **Ações Rápidas:** Cópia facilitada de endereços IPv4 primários/secundários ou URLs DoH para configuração de rede.

---

## 📊 Histórico e Exportação

* **Base de Dados Local:** Armazenamento em SQLite com retenção configurável (1 a 365 dias).
* **Exportação:** Geração de relatórios em formato `.xlsx` (Excel) com folhas detalhadas de testes e resumos estatísticos.
* **Gestão de Dados:** Eliminação granular de registos individuais ou limpeza total do histórico com confirmação.

---

## ⚙️ Aspeto e Sistema

* **Interface Fluent Design:** Suporte para tema Claro, Escuro ou sincronizado com o Windows.
* **Identidade Visual:** Gráficos e indicadores com esquemas de cores dedicados para download (`#00E5FF`) e upload (`#10B981`).
* **Multi-idioma:** Disponível em Português, Inglês, Espanhol, Alemão, Francês e Italiano.
* **Integração de Sistema:**
  * Ícone na área de notificação (System Tray) com atalhos rápidos.
  * Opção de arranque com o Windows (`HKCU\...\Run`, sem necessidade de privilégios de Administrador).
  * Fila de testes: Testes agendados à WAN aguardam automaticamente a conclusão de benchmarks LAN ou DNS em curso.
* **Atualizações Automáticas (v2.5):** A app procura novas versões ao arrancar e uma vez por dia (repositório público de instaladores [wan-speed-logger-releases](https://github.com/RickMGPinto/wan-speed-logger-releases/releases)). Com um clique em *Atualizar agora*, descarrega o instalador, confirma a integridade (SHA-256), atualiza em modo silencioso e volta a abrir, mantendo definições e histórico.

---

## 🛠️ Requisitos e Configuração Opcional

* **Windows 10/11**
* **Speedtest CLI (Opcional):**
  ```powershell
  winget install Ookla.Speedtest.CLI
(Requer aceitação prévia dos termos de utilização da Ookla nas Definições da app).
* **Rede Interna: Permitir a porta da aplicação na Firewall do Windows quando conectada a redes com perfil "Privada".

## Dados
`%LOCALAPPDATA%\WAN Speed Logger\` — `results.db`, `settings.json`, `app.log`.
Dados de versões anteriores (`%LOCALAPPDATA%\SpeedMonitor`) são migrados automaticamente.
A desinstalação mantém esta pasta.

## Consumo de dados
O consumo é proporcional à velocidade da ligação e à duração do teste: a ~500/300 Mbps, cerca de
0,4 GB (Leve), 0,9 GB (Normal) ou até 3,6 GB (Completo, LibreSpeed) por teste. O ecrã de
Definições mostra a estimativa diária/mensal para o intervalo e modo escolhidos.
