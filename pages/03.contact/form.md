---
title: Contact
icon: envelope fa-fw
form:
    name: forma-contacto
    fields:
        -
            name: nombre
            label: Name
            placeholder: 'Name'
            autofocus: 'on'
            autocomplete: 'on'
            type: text
            validate:
                required: true
        -
            name: email
            label: Email
            placeholder: 'Email'
            type: text
            validate:
                pattern: '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{1,63}$'
                required: true
        -
            name: telefono
            label: Phone
            type: text
            validate:
                required: true
       
        -
            name: comentarios
            label: Comment
            type: textarea
            validate:
                required: true
        -
            name: g-recaptcha-response
            label: 'Are you a robot?'
            type: captcha
            recatpcha_site_key: 6Lc9SRgTAAAAAKm-B1OgDoco88VAX-WVxFsKSt4k
            recaptcha_not_validated: 'Invalid Captcha!'
            validate:
                required: true
    buttons:
        -
            type: submit
            value: Send
    process:
        -
            save:
                fileprefix: contact-
                dateformat: Ymd-His-u
                extension: txt
                body: '{% include "forms/data.txt.twig" %}'
        -
            email:
                from: '{{ form.value.email|e }}'
                to: '{{ config.plugins.email.to }}'
                subject: '[Contact Cumintj.com] {{ form.value.name|e }}'
                body: '{% include "forms/data.html.twig" %}'
        -
            display: Thank You
---
