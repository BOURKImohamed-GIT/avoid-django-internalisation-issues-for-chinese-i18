# avoid-django-internalisation-issues-for-chinese-i18
avoid django internalisation issues for chinese 

in locale folder ceate second folder with name zh_Hans  (chinese simplify)


in settings.py add this 


LANGUAGES = [
  ('en', _('English')),

 ('zh-hans', _('Simplified Chinese')),
]

LOCALE_PATHS=[
    os.path.join(BASE_DIR,'locale')
]


MIDDLEWARE = [

    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    

    'django.middleware.locale.LocaleMiddleware',  # shoul be here
  
  
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',
]

now go and impoert i18 in all templates and use the gabarit like this to translate : {% trans   'here omethings to translate' %}
py manage.py makemessages -l zh_hans -i  venvname
go to django.go add your tranltae and:
django-admin compilemessages --ignore=cache --ignore=outdated/*/localetrans

now it should work

-to handl laguage switshing :

this is my exemple for tow language en and zh_hans:
 <div class="col-6 col-sm-6 ">
                        
                            <div id="pgdg-language">
                          
                            
                                <button class="collapsible pgdg-lang-active" id="collapsible" onclick="openPgdgLanguage()">
                                
                                    {% trans "language" %}
                                    <i class="fa fa-angle-up"></i></button>
                                <div id="lang-content">
                                    {% get_current_language as LANGUAGE_CODE %}
                                    {% get_available_languages as LANGUAGES %}
                                    {% get_language_info_list for LANGUAGES as languages %}
                                    {% for language in languages %}
                                    {% if language.code == 'en' %}
                                  
                                    <a href="/{{language.code}}/"> <div class="pgdg-hover" ><img src="{% static 'images/flags/en.png' %}" class="pgdg-flag"><span
                                    class="choice"> EN</span>
                                    </div></a>
                            
                                  {% else %} 
                                  
                                    <a href="/{{language.code}}/"> <div class="pgdg-hover" ><img src="{% static 'images/flags/ch.png' %}" class="pgdg-flag"><span
                                     class="choice">CH</span>  
                                
                                    </div></a>
                                  {% endif %}
                                   
                                  {% endfor %}
                                </div>
                            </div>
                    </div>
        


now for translating modeles go to modeltranslation package:
i advice you to use also DJANGO-ROSETTA

good luck

