## Plan: Blog Recente Na Home

Adicionar uma nova seção na página inicial para exibir somente o post mais recente publicado (não draft), posicionada entre Projetos e Tech, com card contendo título, descrição, data e tags. Se não houver post publicado, a seção não deve renderizar.

**Steps**
1. Criar um novo componente de seção em /home/guiribeiro/Projects/portal_guidev/src/components/blog-recent.astro para centralizar layout, estilos e carregamento do conteúdo do blog via Content Collections.
2. No componente, buscar posts com getCollection('blog', ({ data }) => data.draft !== true), ordenar por pubDate decrescente e selecionar apenas o primeiro item (post mais recente).
3. Implementar renderização condicional no componente: se não houver post, retornar nada; se houver, renderizar seção completa com header de seção e card único.
4. Estruturar o card do post com os campos definidos: título, descrição, data formatada pt-BR e tags, com link para /blog/[id], reutilizando o padrão visual existente da listagem de blog para manter consistência visual. *depends on 2*
5. Integrar o componente em /home/guiribeiro/Projects/portal_guidev/src/pages/index.astro, importando e inserindo <BlogRecent /> entre <Projects /> e <Tech />. *depends on 1*
6. Adicionar um CTA secundário “Ver todos os posts” na seção, apontando para /blog, para ampliar a descoberta de conteúdo sem poluir o layout. *depends on 3,4*
7. Validar responsividade e estados visuais (desktop/mobile), garantindo que a nova seção respeite espaçamentos e tipografia já usados na home e mantenha o CTA legível/visível. *depends on 3,4,5,6*
8. Executar validação de build e inspeção manual de navegação para confirmar que o link do card abre corretamente o post mais recente e que o CTA abre /blog. *depends on 7*

**Relevant files**
- /home/guiribeiro/Projects/portal_guidev/src/components/blog-recent.astro — novo componente para buscar e renderizar o post mais recente.
- /home/guiribeiro/Projects/portal_guidev/src/pages/index.astro — import e posicionamento da seção entre componentes existentes.
- /home/guiribeiro/Projects/portal_guidev/src/pages/blog/index.astro — referência de estilo de card e padrões de data/tags para reaproveitar consistência.
- /home/guiribeiro/Projects/portal_guidev/src/content.config.ts — referência de schema dos campos usados no card (title, description, pubDate, tags, draft).

**Verification**
1. Rodar build do projeto e confirmar ausência de erros de tipagem/renderização Astro.
2. Abrir a home e verificar se a seção aparece somente quando existe post com draft=false.
3. Validar no layout mobile e desktop: card legível, sem overflow e com espaçamento consistente.
4. Clicar no card e confirmar navegação para /blog/[id] do post mais recente.
5. Conferir que data e tags do card batem com os metadados do post em src/content/blog.

**Decisions**
- Posição da seção: entre Projetos e Tech.
- Conteúdo do card: título + descrição + data + tags.
- CTA adicional: incluir “Ver todos os posts” com link para /blog.
- Estado vazio: ocultar totalmente a seção quando não houver post publicado.
- Escopo incluído: apenas 1 post mais recente na home.
- Escopo excluído: listagem de múltiplos posts, paginação e filtros por tag.

**Further Considerations**
1. Recomendação futura: considerar campo cover opcional no card quando houver imagem de capa para enriquecer visualmente a home.