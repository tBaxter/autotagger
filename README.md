Autotagger
=====

Autotagger helps automatically create text links between related objects in Django applications as well as cross-reference by arbitrary admin-defined strings.

Takes a given block of text and tags it according to models and fields defined in settings.

### Installation
``` pip install tango-autotagger ```

### SETUP

Example:
    
    AUTOTAG_CONTENT = (
      {
        'model'      : 'schools.school',
        'field'      : 'school',                
        'check'      : 'is_active',               
        'm2m_field'  : 'articles',
        'reverse_m2m': 'politicians',
       },
       ... etc ...
    )
    

THE FIELDS...

    model: 
        the app and model to check
    field:
        the particular field/value you are matching in the text
    check:
        an optional field to filter by. Maybe. If we can figure out how to do it...
    m2m_field:
        Optional. Will add the current object to a m2m field on the remote object.
        For example, if you are auto_tagging schools in articles
        you can add the article to the schools "articles" field.
    reverse_m2m:
        Optional. Will add the remote object to a m2m field on the current object.
        For example, politicians can be a m2m on articles in some cases.
        If you were tagging politicians in articles, this would add the politician
        to the article's  "politicians" field.
        
Do NOT attempt to use both m2m and reverse_m2m on the same setting.

To insert links to matching objects:

   from autotagger.autotag_content import autotag
 
   tagged_text = autotag(article.text)

