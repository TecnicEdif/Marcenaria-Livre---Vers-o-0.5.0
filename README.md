# Marcenaria-Livre---Vers-o-0.5.0
Ferramenta open-source para projeto de ambientes, criação de móveis planejados, geração automática de listas de peças (plano de corte), orçamentos e pranchas técnicas no Linux. | Open-source tool for room design, custom furniture creation, automatic parts list generation (cutting plan), budgeting, and technical sheets on Linux.

Principais Recursos: 

Modelagem de Ambientes: Construção intuitiva de paredes retas, contínuas e curvas, além de portas, janelas, pisos e rebaixos de gesso.   

Biblioteca e Criador de Módulos: Ampla variedade de móveis parametrizados para cozinhas, banheiros, dormitórios, escritórios e painéis (como painéis ripados e para TV). 

Plano de Corte e Orçamento: Geração heurística de chapas, cálculo de fitas de borda, ferragens e estimativa completa de custos e mão de obra.   

Documentação Técnica: Editor de pranchas A4 com cotas automáticas, vistas ortogonais (1:25) e exportação para PDF, SVG, CSV e IFC4 (BIM).   

Organização e Camadas: Sistema de controle por categorias com bloqueio e proteção de colisão entre volumes.   

🐧 Compatibilidade no LinuxDisponível em pacotes compatíveis na pasta dist (AppImage, .deb e Flatpak com runtime Freedesktop 25.08, utilizando glibc 2.39 ou superior).   

⚠️ Nota: Esta é uma versão em desenvolvimento (v0.5.0). Ela tem bugs, erros e ferramentas que não estão funcionando da forma correta. Recomenda-se conferir medidas, encaixes e listas de fabricação antes da produção física. 

# Marcenaria Livre 0.5.0

Aplicativo de projeto de ambientes e marcenaria em Rust, com interface gráfica, fabricação, orçamento, plano de corte e pranchas. Versão em desenvolvimento, com limitações descritas abaixo.

## Começar

Use o AppImage, Debian `.deb` ou Flatpak em `dist` na entrega completa. Os binários Linux x86_64 desta entrega exigem glibc 2.39 ou superior. O Flatpak usa Freedesktop 25.08. Salve projetos editáveis em `.mar`. Os manuais em português, inglês e espanhol ficam em `docs/manuais`.

## Novidades

- Ctrl+C, Ctrl+V, Ctrl+A, Ctrl+G e Shift+G; seleção com Ctrl+clique; menu Editar e matriz com até 200 cópias por operação. Grupos persistem no projeto e no desfazer.
- Painel ripado e painel para TV com criadores separados, prévia, medidas, posição e material. Peças de ripados entram na lista de fabricação.
- Gesso liso, perimetral e escalonado; rodapés decorativos com três perfis, posicionamento superior/inferior, medidas e corte esquemático.
- Geometria decorativa por contorno simples e extrusão vertical, com prévia e arraste para alterar a altura; exportação de perfil extrudado em IFC.
- Módulos com portas externas, gavetas internas inferiores e prateleiras superiores; topo completo, sem topo ou duas travessas.
- Mais 15 inferiores de cozinha sem topo, 15 de banheiro sem topo, 10 nichos para forno e 20 módulos de escritório.
- Decoração organizada em categorias, com mais 200 variações dimensionais de oito famílias paramétricas. Modelos de mesas, bancos e estantes dessas famílias possuem peças representadas separadamente.
- Dez novos acabamentos aproximados de vidro; frentes de vidro com perfis horizontais e verticais.
- Importação local de texturas PNG para materiais de módulos e painéis. As imagens são referenciadas pelo caminho, não embutidas no `.mar`; acompanhe os arquivos ao transferir um projeto.
- Troca de modelos decorativos de portas/janelas nas propriedades, posição na parede por valor e arraste em planta/3D. Representação simplificada de venezianas, perfis, frentes provençais e travessas.
- Parede curva calculada por três pontos e dividida em trechos de até 2 graus, agrupados.
- Seleção 3D por faces para módulos, paredes, aberturas, painéis, decoração e gesso. Contornos de seleção múltipla, ampliação da faixa de zoom e reaproveitamento de imagens sem alterações. Resolução temporariamente reduzida durante movimento.
- Código de preparação de builds Windows/macOS em `packaging`, sem binários compilados nessas plataformas. Complementos externos removidos do código ativo e desta entrega.

## Limites e pontos ainda pendentes

- Não foram incorporadas as 200 texturas oficiais dos fabricantes solicitados. Não há pacote de imagens autorizado para redistribuição. Materiais padrão são cores e veios aproximados; não são texturas oficiais. Consulte `docs/MATERIAIS.md`.
- A modelagem decorativa é uma extrusão de contorno simples; não é modelagem livre de cada face, não faz furos nem operações booleanas.
- Grupos propagam translação a partir de módulos, painéis ou decoração. Rotação e escala conjuntas ainda não são implementadas. A matriz é linear no vetor X/Y/Z, não circular nem uma grade independente de linhas e colunas.
- O arco usa trechos; ainda falta uma entidade curva única com raio editável. Uma abertura não atravessa vários trechos de curva.
- Rodapés possuem extremidades recuadas. Encontros de cantos e recortes em portas exigem revisão manual; a ferramenta não resolve automaticamente todas as junções.
- Colisões usam volumes externos conservadores, não cavidades internas. Podem impedir encaixes legítimos de objetos dentro de nichos. Portas em movimento não possuem simulação física completa.
- Os modelos de esquadrias são simplificados. A troca de modelo não simula todos os mecanismos reais. Bibliotecas contêm variações paramétricas, não centenas de modelos artísticos independentes.
- Espessuras, folgas, montagem do fundo e regras de fabricação precisam ser conferidas em relação à representação 3D antes de produzir. Não há garantia de fabricação sem revisão.
- Reflexo e brilho não constituem um renderizador físico; paredes e pisos têm representação simplificada. Texturas PNG não são incorporadas ao IFC.
- Tradução da interface é parcial; os três manuais são traduzidos. Recursos recentes ainda exibem português na interface.
- CSV para serviços externos é genérico, com mapeamento de colunas e conferência necessários.
- O pacote Snap não foi construído; há uma receita. Windows/macOS incluem fontes e scripts não executados, com seletores de arquivos ainda dependentes do Linux.

## Compilar

Instale Rust/Cargo e bibliotecas gráficas Linux X11, xkbcommon e OpenGL. Execute `cargo build --release`; testes: `cargo test --release`. O seletor de arquivos usa Zenity. `cargo fmt` organiza o código.

O código está em `src`. `tools/validate_ifc.py` usa IfcOpenShell para validar estrutura e reconstruir sólidos. `tools/build_manuals.py` requer ReportLab, Pillow e fontes DejaVu. As receitas Linux estão em `packaging` e `snap`; scripts de portabilidade em `packaging/windows` e `packaging/macos`.

A entrega de código usa uma lista explícita de arquivos públicos e não inclui caches, credenciais, histórico de conversa nem projetos particulares. A licença e a identificação do autor estão em `LICENSE`. Instaladores devem ser anexados a uma release; a publicação no GitHub não foi feita automaticamente.

Main FeaturesRoom Modeling: 

Intuitive construction of straight, continuous, and curved walls, as well as doors, windows, floors, and plaster drop ceilings.   

Library and Module Creator: Wide variety of parameterized furniture for kitchens, bathrooms, bedrooms, offices, and panels (such as slatted panels and TV panels).   

Cutting Plan and Budget: Heuristic sheet generation, edge banding calculation, hardware estimation, and complete cost and labor estimation.   

Technical Documentation: A4 sheet editor with automatic dimensions, orthogonal views (1:25), and export to PDF, SVG, CSV, and IFC4 (BIM).   

Organization and Layers: Category-based control system with locking and collision protection between volumes.   

Linux CompatibilityAvailable in compatible packages in the dist folder (AppImage, .deb, and Flatpak with the Freedesktop 25.08 runtime, using glibc 2.39 or higher).   

Note: This is a version in development (v0.5.0). It is recommended to check measurements, fittings, and manufacturing lists before physical production. 

Marcenaria Livre 0.5.0
Room and woodworking design application written in Rust, featuring a graphical interface, manufacturing lists, budgeting, cutting plans, and technical sheets. This is a version in development, with the limitations described below.

Getting Started
Use the AppImage, Debian .deb, or Flatpak located in the dist folder within the full release. The Linux x86_64 binaries in this release require glibc 2.39 or higher. The Flatpak uses the Freedesktop 25.08 runtime. Save editable projects in .mar format. Manuals in Portuguese, English, and Spanish are located in docs/manuais.

What's New
Ctrl+C, Ctrl+V, Ctrl+A, Ctrl+G, and Shift+G shortcuts; selection via Ctrl+click; Edit menu, and a matrix tool supporting up to 200 copies per operation. Groups persist in the project and through undo actions.

Slatted panels and TV panels featuring separate creators, previews, dimensions, positions, and materials. Slatted panel parts are included in the manufacturing list.

Flat, perimeter, and stepped plaster drop ceilings; decorative baseboards with three profiles, top/bottom positioning, dimensions, and schematic cuts.

Decorative geometry created via simple contours and vertical extrusion, with a preview and dragging capability to modify height; export of extruded profiles in IFC.

Modules with external doors, lower internal drawers, and upper shelves; full top, top-less, or two-crossbar options.

15 additional top-less lower kitchen modules, 15 top-less bathroom modules, 10 oven niches, and 20 office modules.

Decoration organized into categories, featuring over 200 dimensional variations across eight parametric families. Models of tables, benches, and bookshelves from these families have their parts represented separately.

Ten new approximate glass finishes; glass frames with horizontal and vertical profiles.

Local import of PNG textures for module and panel materials. Images are referenced by path rather than embedded within the .mar file; make sure to accompany files when transferring a project.

Replacement of decorative door/window models within properties, positioning on walls by value, and dragging in 2D/3D views. Simplified representation of louvers, profiles, Provençal fronts, and crossbars.

Curved walls calculated using three points and divided into grouped segments of up to 2 degrees.

3D face selection for modules, walls, openings, panels, decoration, and plaster elements. Multi-selection outlines, expanded zoom range, and reuse of images without alterations. Resolution is temporarily reduced during movement.

Windows/macOS build preparation code in packaging, without compiled binaries for those platforms. External add-ons removed from active code and this release.

Limits and Pending Points
The 200 official textures from requested manufacturers were not incorporated. There is no authorized image package for redistribution. Standard materials are approximate colors and woodgrains, not official textures; consult docs/MATERIAIS.md.

Decorative modeling is a simple contour extrusion; it does not support free-form modeling of individual faces, hole-making, or Boolean operations.

Groups propagate translation starting from modules, panels, or decoration. Joint rotation and scaling are not yet implemented. The matrix tool is linear along the X/Y/Z vectors and is not circular or an independent grid of rows and columns.

Arcs use segments; a single curved entity with an editable radius is still missing. An opening cannot cross multiple curve segments.

Baseboards have recessed ends. Corner joints and door cutouts require manual revision; the tool does not automatically resolve all junctions.

Collisions use conservative external volumes rather than internal cavities, which may prevent legitimate placement of objects inside niches. Moving doors lack full physical simulation.

Millwork models are simplified. Model swapping does not simulate all real mechanical actions. Libraries contain parametric variations rather than hundreds of independent artistic models.

Thicknesses, clearances, back-assembly, and manufacturing rules must be checked against the 3D representation before production. There is no guarantee of fabrication without review.

Reflection and gloss do not constitute a physical renderer; walls and floors have a simplified representation. PNG textures are not embedded into IFC files.

Interface translation is partial; the three manuals are fully translated. Recent features still display Portuguese in the interface.

CSV exports for external services are generic and require column mapping and verification.

The Snap package has not been built, though a recipe is provided. Windows/macOS packages include unexecuted sources and scripts, with file pickers still dependent on Linux.

Build Instructions
Install Rust/Cargo along with Linux X11, xkbcommon, and OpenGL graphic libraries. Run cargo build --release; run tests with cargo test --release. The file picker uses Zenity. Use cargo fmt to organize code.

The source code is located in src. tools/validate_ifc.py uses IfcOpenShell to validate structure and reconstruct solids. tools/build_manuals.py requires ReportLab, Pillow, and DejaVu fonts. Linux recipes are located in packaging and snap, with portability scripts in packaging/windows and packaging/macos.

The code release uses an explicit list of public files and excludes caches, credentials, chat history, and private projects. The license and author identification are located in LICENSE. Installers must be attached to a release; publishing to GitHub was not done automatically.
