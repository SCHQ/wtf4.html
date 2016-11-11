# wtf4.html
wtf.html (Flask-wtf & Flask-bootstrap) adapted for Bootstrap4 styles. 




## Purpose
To quickly render out form with latest Bootstrap4 styes, by customized wtf.html (part of Flask-Bootstrap)

![](http://img.blog.csdn.net/20161111105913670?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

[Live Demo](http://tianya.heroku.com/about)



## Background
We know Flask-bootstrap provides a macro to quickly render out a form by one line:
> /app/forms.py
```
class CommentForm(Form):
  ...

/tempelate/about.html:
{% import "bootstrap/wtf.html" as wtf %}
        {{ wtf.quick_form(form, button_map={'submit':'primary'} }}
```
But it's a bit simple, although you can add customized CSS in forms.by like below, but it's not adapted for Bootstrap4 (Alpha5).
```
class CommentForm(Form):
    name = StringField('', validators=[Length(0, 64)], render_kw={"placeholder": "your name",
                                                                  "style": "background: url(/static/login-locked-icon.png) no-repeat 15px center;text-indent: 28px"})
    email = StringField('', description='* We\'ll never share your email with anyone else.', validators= \
        [DataRequired(), Length(4, 64), Email(message=u"邮件格式有误")], render_kw={"placeholder": "yourname@example.com"})
    comment = TextAreaField('', description=u"请提出宝贵意见和建议", validators=[DataRequired()],
                            render_kw = {"placeholder": "Input your comments here"})
    submit = SubmitField(u'提交')
```
The styles and format of form are defined in wtf.html, it's in your Flask-bootstrap install directly. 
e.g.: *C:\git\tianya\venv\Lib\site-packages\flask_bootstrap\templates\bootstrap\wtf.html

## Install and how to use
1. simple copy my _wtf4.html to you Flask template directly
*C:\git\tianya\app\templates\
2. use the macro in your html like this
> /tempelate/about.html
```
{% import "_wtf4.html" as _wtf4 %}
{% block page_content %}

<div id="comment_div" class="row comment-form" style="margin-top: 80px">
<div class="col-lg-6 offset-lg-3">
 <h3 class="panel-title">
    <a href="#" ><i class="fa fa-pencil">&nbsp</i>留言板</a></h3>
        {{ _wtf4.quick_form(form, form_type="basic", button_map={'submit':'primary', }, id='comment_form') }}
</div>
</div>
```
3. design your form
> /app/forms.py
```
class CommentForm(Form):
    name = StringField('', validators=[Length(0, 64)], render_kw={"placeholder": "your name",})
    email = StringField('', description='* We\'ll never share your email with anyone else.', validators= \
        [DataRequired(), Length(4, 64), Email(message=u"邮件格式有误")], render_kw={"placeholder": "yourname@example.com"})
    comment = TextAreaField('', description=u"* 请提出宝贵意见和建议", validators=[DataRequired()],
                            render_kw = {"placeholder": "input your comments here"})
    submit = SubmitField(u'提交')
    # FontAwesome css, show icon as prefix of fields
    fa_addon = {
        'email': 'fa-envelope-o',
        'name': 'fa-user-o',
    }
```
fa_addon is used as icons for every input field, needs [FontAwesome CSS](http://fontawesome.io/examples/), you can add the CDN in your html like this:
```
<link rel="stylesheet" type="text/css" href="//cdn.bootcss.com/font-awesome/4.7.0/css/font-awesome.css">
```

## make your own wtf.html
I've adapted for the following CSS:
```
class="input-group-addon"
class="form-text text-muted"
class="form-text text-warning">
```
You can add/change any more CSS as you want, in _wtf4.html
