---
# Leave the homepage title empty to use the site title
title:
date: 2022-10-24
type: landing

sections:
  - block: hero
    content:
      title: Personal website of Tigran (TIKSN) Torosyan
      image:
        filename:
      cta:
        label:
        url:
      cta_alt:
        label:
        url:
      cta_note:
        label: >-
          [![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://stand-with-ukraine.pp.ua)
      text:
    design:
      background:
        gradient_end: '#1976d2'
        gradient_start: '#004ba0'
        text_color_light: true
  - block: about.biography
    id: about
    content:
      title: Biography
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: tiksn
  - block: features
    content:
      title: Skills
      items:
          - description: 100%
            icon: microsoft
            icon_pack: fab
            name: C# / .NET / ASP.NET / EF
          - description: 100%
            icon: cogs
            icon_pack: fas
            name: Microservices / Docker / Kubernetes
          - description: 80%
            icon: terminal
            icon_pack: fas
            name: PowerShell
          - description: 80%
            icon: envelope
            icon_pack: fas
            name: Apache Kafka / RabbitMQ
          - description: 75%
            icon: database
            icon_pack: fas
            name: MongoDB / Redis
          - description: 70%
            icon: database
            icon_pack: fas
            name: SQL Server / PostgreSQL
  - block: portfolio
    id: projects
    content:
      title: Projects
      filters:
        folders:
          - project
      # Default filter index (e.g. 0 corresponds to the first `filter_button` instance below).
      default_button_index: 0
      # Filter toolbar (optional).
      # Add or remove as many filters (`filter_button` instances) as you like.
      # To show all items, set `tag` to "*".
      # To filter by a specific tag, set `tag` to an existing tag name.
      # To remove the toolbar, delete the entire `filter_button` block.
      buttons:
        - name: All
          tag: '*'
        - name: .NET
          tag: dotnet
        - name: C#
          tag: csharp
        - name: F#
          tag: fsharp
        - name: PowerShell
          tag: powershell
        - name: Python
          tag: python
        - name: Go
          tag: go
    design:
      # Choose how many columns the section has. Valid values: '1' or '2'.
      columns: '1'
      view: showcase
      # For Showcase view, flip alternate rows?
      flip_alt_rows: false
  - block: tag_cloud
    content:
      title: Popular Topics
    design:
      columns: '2'
  - block: contact
    id: contact
    content:
      title: Contact
      subtitle:
      text:
      # Contact (add or remove contact options as necessary)
      email:
      phone:
      appointment_url:
      address:
        street:
        city:
        region:
        postcode:
        country:
        country_code:
      directions:
      office_hours:
      contact_links:
        - icon: twitter
          icon_pack: fab
          name: DM Me
          link: 'https://twitter.com/tiksn'
        - icon: skype
          icon_pack: fab
          name: Skype Me
          link: 'skype:akatiksn?call'
        - icon: linkedin
          icon_pack: fab
          name: Connect on LinkedIn
          link: 'https://www.linkedin.com/in/tiksn'
        - icon: keybase
          icon_pack: fab
          name: Chat on Keybase
          link: 'https://keybase.io/tiksn'
      # Automatically link email and phone or display as text?
      autolink: true
      # Email form provider
      form:
        provider: netlify
        formspree:
          id:
        netlify:
          # Enable CAPTCHA challenge to reduce spam?
          captcha: true
    design:
      columns: '2'
---
