# Django - django.views.generic包的变化 #
##      django 通用视图##
---
### direct_to_template ###
Django 1.3 以前

    from django.conf.urls.defaults import *
    from django.views.generic.simple import direct_to_template
    **from mysite.books.views import about_pages**
    urlpatterns = patterns('',
        ('^about/$', direct_to_template, { 'template': 'about.html'}),
        **('^about/(w+)/$', about_pages),**
    )

Django 1.4 以后弃用这种做法，改用TemplateView.as_view()

    Django 1.7写法：
    from django.conf.urls import patterns, url
    from django.views.generic import TemplateView
    from mysite.books.views import about_pages
    urlpatterns = patterns('',
        url(r'^about/$', TemplateView.as_view(template_name='about.html'),
        ('^about/(w+)/$', about_pages),
    )

---
