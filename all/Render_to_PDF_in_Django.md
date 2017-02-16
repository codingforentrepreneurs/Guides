![Render to PDF Logo](https://cfe2-static.s3-us-west-2.amazonaws.com/media/cfe-blog/html-template-to-pdf-in-django/render_to_pdf_share.png)
Render to PDF in Django
=====

A guide to using an HTML template to create a PDF via a `render_to_pdf` utility function.


1. Open your Django project or [create a blank one](https://www.codingforentrepreneurs.com/blog/create-a-blank-django-project/)

2. Install `xhtml2pdf` [docs](https://github.com/xhtml2pdf/xhtml2pdf):

    Using Python 3
    ```
    pip install --pre xhtml2pdf 
    ```
    Using Python 2
    ```
    pip install xhtml2pdf
    ```

2. Add a `utils.py` module  to your project:

3. Write the `render_to_pdf` function:
    ```
    from io import BytesIO
    from django.http import HttpResponse
    from django.template.loader import get_template
    
    from xhtml2pdf import pisa
    
    def render_to_pdf(template_src, context_dict={}):
        template = get_template(template_src)
        html  = template.render(context_dict)
        result = BytesIO()
        pdf = pisa.pisaDocument(BytesIO(html.encode("ISO-8859-1")), result)
        if not pdf.err:
            return HttpResponse(result.getvalue(), content_type='application/pdf')
        return None

    ```

4. Create html template such as `invoice.html` in `templates/pdf` ** Recommended to use internal/inline stylesheets** :
    ```
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
        <head>
            <title>Title</title>
            <style type="text/css">
                body {
                    font-weight: 200;
                    font-size: 14px;
                }
                .header {
                    font-size: 20px;
                    font-weight: 100;
                    text-align: center;
                    color: #007cae;
                }
                .title {
                    font-size: 22px;
                    font-weight: 100;
                   /* text-align: right;*/
                   padding: 10px 20px 0px 20px;  
                }
                .title span {
                    color: #007cae;
                }
                .details {
                    padding: 10px 20px 0px 20px;
                    text-align: left !important;
                    /*margin-left: 40%;*/
                }
                .hrItem {
                    border: none;
                    height: 1px;
                    /* Set the hr color */
                    color: #333; /* old IE */
                    background-color: #fff; /* Modern Browsers */
                }
            </style>
        </head>
        <body>
            <div class='wrapper'>
                <div class='header'>
                    <p class='title'>Invoice # </p>
                </div>
            <div>
            <div class='details'>
                Bill to: <br/>
                Amount:  <br/>
                Date: 
                <hr class='hrItem' />
            </div>
        </div>
        </body>
    </html>
    ```

5. Use in a view:
    ```
    from django.http import HttpResponse
    from django.views.generic import View

    from yourproject.utils import render_to_pdf #created in step 4

    class GeneratePdf(View):
        def get(self, request, *args, **kwargs):
            data = {
                 'today': datetime.date.today(), 
                 'amount': 39.99,
                'customer_name': 'Cooper Mann',
                'order_id': 1233434,
            }
            pdf = render_to_pdf('pdf/invoice.html', data)
            return HttpResponse(pdf, content_type='application/pdf')

    ```

6. Force PDF Download:
    ```
    class GeneratePDF(View):
        def get(self, request, *args, **kwargs):
            template = get_template('invoice.html')
            context = {
                "invoice_id": 123,
                "customer_name": "John Cooper",
                "amount": 1399.99,
                "today": "Today",
            }
            html = template.render(context)
            pdf = render_to_pdf('invoice.html', context)
            if pdf:
                response = HttpResponse(pdf, content_type='application/pdf')
                filename = "Invoice_%s.pdf" %("12341231")
                content = "inline; filename='%s'" %(filename)
                download = request.GET.get("download")
                if download:
                    content = "attachment; filename='%s'" %(filename)
                response['Content-Disposition'] = content
                return response
            return HttpResponse("Not found")
    ```


### Watch [here](https://www.codingforentrepreneurs.com/projects/render-pdf/)
<iframe width="560" height="315" src="https://www.youtube.com/embed/B7EIK9yVtGY" frameborder="0" allowfullscreen></iframe>
