# Macaé — A cidade em uma linha

Edição de 22/10/2026, desenvolvida sobre o projeto existente após aprovação da direção C, com a materialidade de A e uma passagem espacial de B. A abertura mantém o nome da exposição: **Macaé — uma história em movimento**.

## O que mudou

A linha agora tem geometria editorial própria para cada capítulo. Atravessa o alto do porto, contorna a composição e encontra dois traços paralelos sob a ferrovia. São metáforas gráficas de conexão, não representações de rotas ou limites históricos. A faísca percorre o comprimento real desse caminho, e a névoa acompanha sua posição.

Na abertura, um percurso luminoso revela o nome MACAÉ e se liga à timeline. Em 1813 e 1846, a data chega em escala maior e encontra sua posição de leitura. O petróleo recebe data monumental e um enquadramento próprio para fotografias pequenas. O encerramento recupera o título sem cruzar suas letras com a linha.

A passagem do porto para a ferrovia dura três segundos: o último registro que estava em exibição permanece na frente, uma reprodução identificada da estação de 1917 aparece por baixo, o rasgo ganha uma dobra mais larga, sombra de contato e luz na ruptura. A superfície se aproxima discretamente em perspectiva. Os créditos distinguem o mapa de 1846 ou a foto de 1941 da fotografia ferroviária de 1917. A navegação manual preserva o registro realmente exibido antes da passagem.

As imagens ficam estáveis por quatro segundos por posição, além do rasgo. O capítulo de imagem única recebe 4,8 s; abertura, 6 s; encerramento, 5 s. O ciclo nominal é aproximadamente 95,74 s. Autoplay e loop continuam ativos. Tudo é conduzido pelo mesmo relógio de apresentação, incluindo pausa, tipografia, luz, rasgo, viagem e reinício.

## Roteiro visual

| Momento | Composição e movimento |
| --- | --- |
| Abertura | MACAÉ é revelado pela passagem do filamento; o percurso se curva e encontra a linha vertical |
| Pescadores | Documento grande à direita, título à esquerda, observação de três registros autênticos de épocas identificadas |
| Vila | Mapa à esquerda; 1813 em escala grande à direita, com dia e mês preservados |
| Cidade | 1846 conduz a leitura; fotografia posterior à direita e data real explícita |
| Porto | Reprodução maior à esquerda; título à direita; linha horizontal no alto, distante do documento |
| Porto → ferrovia | Uma única passagem espacial de três segundos, com dois registros reais e rasgo iluminado |
| Ferrovia | Fotografia à direita; dois traços editoriais sob a composição sugerem conexão |
| Petróleo | 1978–1980 em destaque; três fotografias com tamanho nativo preservado |
| SESI/SENAI | Composição aberta, fotografia maior e redução da intensidade visual |
| Encerramento | Retorno de MACAÉ, cortina escura e reinício sem recarregar a página |

## Revisão visual realizada

Foram feitas três rodadas, registradas em `round-1`, `round-2` e `round-3`. Cada rodada contém as nove cenas em 1920×1080, cinco estados da passagem, entradas da abertura/datas/petróleo e uma captura do SENAI em 3840×2160.

1. A primeira rodada identificou a linha sobre o título do encerramento e uma iluminação lateral separada da moldura. A linha foi encurtada nesse ponto, a identificação discreta do porto deixou de interferir no traço e o reflexo foi ligado à própria moldura.
2. A segunda refinou o rasgo. O gradiente da dobra passou a seguir a inclinação da ruptura, eliminando a faixa plana de cor. A verificação geométrica encontrou um falso positivo porque media a largura inteira dos blocos de texto; foi corrigida para medir os caracteres efetivamente desenhados. O teste mantém a exigência de nenhuma interseção da linha com os títulos.
3. A terceira corrigiu continuidade: a seção anterior agora conserva a última imagem durante a saída. A passagem usa o registro realmente visível, inclusive ao avançar manualmente. Seu suporte tem altura limitada para não criar uma moldura vazia desproporcional em 4K. As capturas e a montagem reduzida foram revistas depois dessas mudanças.

`round-3/overview.jpg` mostra o conjunto final. Os dados de geometria e erros estão em `inspection.json` de cada rodada. Os registros e os pixels das imagens são idênticos aos do backup; a comparação dos 16 arquivos de catálogo e mídia está em `preservation.json`.

## Arquitetura editável

| Arquivo | Responsabilidade |
| --- | --- |
| `src/motion/choreography.ts` | Caminho, marcos e identificação da passagem especial; geometria decorativa |
| `src/beyond.css` | Composições, datas, abertura, iluminação e suporte da passagem |
| `src/engine/Presentation.ts` | Relógio único, sequência, pausa, retenção da origem, duração da passagem e loop |
| `src/components/PortPassage.tsx` | Seleção dos registros reais e sua apresentação espacial |
| `src/components/PaperTearTransition.tsx` | Folhas, curvatura, fibras, luz e sombra da ruptura |
| `src/motion/config.ts` | Tempos, partículas e controle dos efeitos |
| `src/data/presentation.ts` | Datas e títulos exibidos; contagem das posições de mídia |
| `src/data/events.ts` | Pesquisa, sequência dos sete temas e ressalvas históricas |
| `data/image-sources.json` | Procedência, data real das imagens e condições de uso |

Não foram instaladas novas bibliotecas. O trabalho usa React, TypeScript, SVG, Canvas 2D e transformações de perspectiva em CSS. O rasgo é uma aproximação gráfica em camadas, não uma simulação física de papel. Não foram animados personagens ou objetos dentro das fotografias.

Para alterar textos, edite `presentation.ts`; para substituir imagens, siga `docs/media-guide.md` e atualize os metadados. Para pausas e velocidade, edite `motion/config.ts`. A passagem especial tem duração própria (`PORT_PASSAGE_DURATION`), restaurando a velocidade normal no capítulo seguinte.

## Validação e limites

Os **18 testes passaram**, sem falhas, testes ignorados ou resultados instáveis, conforme o relatório Playwright extraído em `test-summary.json`. Além dos testes anteriores, há verificações da duração especial, pausa e interrupção da passagem, continuidade do documento anterior, geometria sem atravessar títulos em 1080p/4K, respeito à resolução nativa e alternativa com movimento reduzido. O HTML de produção não expõe os controles internos de inspeção.

A gravação normal, os dados de desempenho e os testes do HTML offline estão na pasta `final`. A amostragem de desempenho inclui rasgos comuns e a passagem especial. O polimento final estabiliza a perspectiva antes da maior parte da ruptura, reduz os vértices somente nessa passagem e substitui o blur dinâmico por luz em camadas. O ensaio acelerado monitora 12 ciclos, ouvintes, DOM, partículas e heap. Não equivale a uma sessão de várias horas numa TV física.

As fontes e condições de uso continuam disponíveis pela tecla S. Os sete registros com autorização declarada pelo responsável não foram convertidos em licenças públicas nem em autorizações verificadas de forma independente. As datas provisórias anteriores continuam provisórias; esta edição não acrescentou alegações históricas. A estação ausente de 1978 permanece documentada e não foi substituída pela de 1917.

Algumas fotos e o primeiro documento têm resolução limitada. Foram preservados os tamanhos nativos: esses registros ocupam menos espaço relativo em 4K. O projeto não inventa detalhes nem usa aumento por IA. A apresentação animada no painel do ChatGPT continua indisponível neste ambiente.

## Exibir na TV

Execute `npm run export` para gerar `exports/macae-alem-da-linha.html`. O arquivo inclui imagens, fontes, estilos, código e créditos. Abra no Chrome ou Edge e pressione **F**. Não é necessário instalar Node ou manter internet na TV. **Espaço** pausa, **←/→** navegam, **R** reinicia, **H** abre controles e **S** abre fontes.

O navegador gerenciado bloqueia navegação direta `file://`; a validação offline usa os bytes exatos exportados com a rede desabilitada. A abertura por duplo clique deve ser conferida no computador da TV. Para editar o projeto: `npm ci`, `npm run dev` e depois novo `npm run export`. `python scripts/package-delivery.py` monta os pacotes de exibição e de fontes e verifica CRC e identidade do HTML.

O pacote editável inclui o código completo, as mídias locais, os relatórios textuais, as montagens das três rodadas e as capturas/vídeo finais. As capturas individuais intermediárias e o backup integral permanecem no workspace.

## Resultados finais

- Ciclo normal gravado, sem interação: **97,553 segundos**, ordem `0,1,2,3,4,5,6,7,8,0`, 537 quadros registrados, zero erros de JavaScript e zero requisições externas.
- **18 testes aprovados**, zero falhas, testes ignorados ou instabilidade.
- Exportação, produção e documento offline: aprovados; imagens e fontes incorporadas, 17 links de créditos, fullscreen e loop funcionando. A navegação direta `file://` não foi testada por restrição do navegador gerenciado.
- Amostra de 9,6 segundos, incluindo a passagem: **55,1 fps** médios; mediana 16,7 ms, percentil 95 de 33,3 ms, pior quadro de 50 ms. Antes do polimento, a amostra registrou 53 fps e pior quadro de 83,2 ms. São medidas do ambiente de teste, sem garantia de 60 fps na TV.
- Após 12 ciclos acelerados: **581 elementos, 8 ouvintes**, sem crescimento entre as medições; heap após coleta passou de 7.951.788 para 7.897.028 bytes. A população de partículas e os 225 fragmentos estáticos da linha permaneceram limitados.

Os resultados brutos estão em `final/validation-results.json`, `final/cycle-results.json` e `final/performance-results.json`. As montagens `final/passage-film-frames.jpg` e `final/loop-film-frames.jpg` foram extraídas do vídeo real e inspecionadas. O vídeo de auditoria amostra quadros; o FPS da apresentação foi medido separadamente no navegador.
