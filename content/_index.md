---
# Leave the homepage title empty to use the site title
title:
date: 2024-10-14
type: landing

sections:
  - block: hero
    content:
      title: |
        CREx:
        Engineering support for ILCB research projects.
      image:
        filename: ILCB_logo_squared_web.png
      text: |
        <br>
        
        The CREx (Centre de Ressources pour l'Experimentation) is composed of a team of engineers specialized in data analysis and scientific computing. Within the perimeter they apply this expertise to support studies on language and communication. The acquisition, processing and analysis of neurophysiological, neuroimaging and behavioural data (fMRI, EEG, MEG and eye-tracking) forms the core of their work. 
  
  - block: collection
    content:
      title: Overview of EEG Projects
      subtitle:
      text:
      count: 5
      filters:
        author: ''
        category: ''
        exclude_featured: false
        publication_type: ''
        tag: ''
      offset: 0
      order: desc
      page_type: post
    design:
      view: card
      columns: '3'
  
  - block: markdown
    content:
      title:
      subtitle: ''
      text:
    design:
      columns: '1'
      background:
        image: 
          filename: coders.jpg
          filters:
            brightness: 1
          parallax: false
          position: center
          size: cover
          text_color_light: true
      spacing:
        padding: ['20px', '0', '20px', '0']
      css_class: fullscreen

  - block: collection
    content:
      title: Latest Preprints
      text: ""
      count: 5
      filters:
        folders:
          - publication
        publication_type: 'article'
    design:
      view: citation
      columns: '1'

  - block: markdown
    content:
      title:
      subtitle:
      text: |
        {{% cta cta_link="./people/" cta_text="Meet the team →" %}}
    design:
      columns: '1'
---
