# Correção da entrada das seções — 22/10/2026

O conteúdo recebia `--entry: 1` durante a viagem. Ao mudar para `SECTION_ACTIVE`, o controlador zerava o progresso e só então iniciava 950 ms de animação. O resultado era a composição aparecer pronta, voltar ao início e se revelar novamente. O retorno manual à abertura também reiniciava sua máscara depois da chegada.

A entrada agora usa os últimos 900 ms da própria viagem. O destino é preparado antes de entrar na tela, o progresso avança sem retroceder e chega a 1 junto com a câmera. A observação mantém os estilos finais. O reflexo da moldura acompanha a aproximação, sem iniciar outra animação depois da parada. Abertura, cortina e traço têm estilos iniciais explícitos para evitar mostrar o estado final antes do primeiro quadro do controlador.

O motor distingue a abertura inicial de uma abertura alcançada por navegação: esta última mantém a revelação concluída. O loop continua reiniciando sob a cortina escura.

Os dois testes de regressão falharam na versão anterior e passaram após a correção. Cobrem cinco viagens (incluindo ida, volta, petróleo e passagem especial), verificam progresso monotônico e estilos estáveis por dois segundos depois da chegada, além do retorno à abertura. A suíte completa e a exportação offline são verificadas antes de gerar os pacotes.

Arquivos alterados: `src/App.tsx`, `src/engine/Presentation.ts`, `src/motion/choreography.ts`, `src/motion/config.ts` e `src/beyond.css`. Testes: `tests/entrance.spec.ts`. Não foram alterados o acervo, as datas ou os textos históricos.

Resultado final: 20 testes passaram. O ciclo automático completo durou 97,541 s, sem erros ou requisições externas. Exportação, documento offline, fullscreen e loop passaram. A montagem `motion-fix/entrada-sem-reinicio.jpg` foi extraída do vídeo real e inspecionada após a correção.
