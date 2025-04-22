

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"> <html> <head> <title>:: Memo Download ::::</title> <meta http-equiv="pragma" content="no-cache"> <meta http-equiv="cache-control" content="no-cache"> <meta http-equiv="expires" content="0"> <meta http-equiv="keywords" content="

pasted

does this  have the source they are getting data from?

Edit
Looking at the HTML document you shared, I can see it's a web page for downloading results memos for Telangana State Board of Intermediate Education (TGBIE) examination results.

The data source isn't explicitly mentioned in the code, but I can see some details about where the form data is submitted:

The form submits to "/bieresultliveNewChanges2025.do" as seen in this line:
<form name="StudentResultForm" method="post" action="/bieresultliveNewChanges2025.do">
Based on various JavaScript functions in the code (like getStudentResult()), it appears the system accesses different database endpoints depending on the year and category selected. The form uses an "actionpart" hidden field that gets set to different values like:
getBieResultFirstYearGen
getBieResultFirstYearVoc
getBieResultSecondYearGen
etc.
These endpoints likely connect to the Telangana State Board of Intermediate Education's database system, though the actual database details aren't visible in the frontend code.

The page appears to be designed and developed by the "Centre for Good Governance" as mentioned in the footer.





i wnt to get same data as that website

Edit
I understand you want to obtain the same data that's accessible through this website (the Telangana State Board of Intermediate Education results system).

To get this data, you have a few options:

Use the official website: The most straightforward and legitimate way is to use the website as intended. Based on the form you shared, you would need:
A valid 10-digit hall ticket number
Select the appropriate year (First or Second)
Choose the category (General, Vocational, General Bridge Course, or Vocational Bridge Course)
The website is for 2025 results specifically
Official API: Check if TGBIE offers an official API for accessing results. Some educational boards provide APIs for legitimate third-party applications.
Web scraping: If you need to collect this data programmatically and there's no official API, you could create a web scraper. However, be aware that:
Web scraping may violate the website's terms of service
The website has multiple security measures (like disabling right-click, preventing back navigation)
You would need to handle form submissions and parse the returned results
If you're considering web scraping, I recommend first checking if there are legitimate ways to access this data through official channels, as educational records are sensitive information.

What specifically are you hoping to do with this data? This would help me provide more tailored advice on the best approach.




image.png
someone is already dong and this is his some part of terminal

Edit
I see that someone has already been accessing the Telangana results data. The image shows HTTP requests to two main endpoints:

/tg_res/fetch-result.php - Likely for first year results
/tg_res/fetch-result._2nd.php - Likely for second year results
These are different from the path shown in the HTML you shared earlier (/bieresultliveNewChanges2025.do), which suggests they've found the actual API endpoints that directly fetch the results.

The log shows a pattern of alternating POST and OPTIONS requests, which is typical for web requests that may involve CORS (Cross-Origin Resource Sharing). The OPTIONS requests are preflight checks before the actual POST requests that fetch the data.

If you want to replicate this approach, you would need:

The correct endpoint URLs (which you now have)
The proper POST parameters to send (hall ticket number, year, category, etc.)
Any required headers or authentication tokens
A Python script using the requests library could be used to make these POST requests. For example:

python
import requests

# For first year results
url = "https://example.com/tg_res/fetch-result.php"
# For second year results 
# url = "https://example.com/tg_res/fetch-result._2nd.php"

data = {
    "hallticket_no": "1234567890",  # 10-digit hall ticket number
    "year": "1",  # 1 for first year, 2 for second year
    "category": "G",  # G for General, V for Vocational, etc.
    "pass_year": "2025"
}

response = requests.post(url, data=data)
if response.status_code == 200:
    print(response.text)  # This would contain the result data
else:
    print(f"Error: {response.status_code}")
Just remember that accessing this data outside the official channels could potentially violate terms of service or potentially raise privacy concerns if you're accessing others' educational records. Be sure you have proper authorization before proceeding.





import requests
from bs4 import BeautifulSoup

# Set the URL where the form posts data
url = 'http://results.cgg.gov.in//bieresultliveNewChanges2025.do'  # Replace <domain> with the actual domain

# Set the form data for the first-year regular student
form_data = {
    'actionpart': 'getBieResultFirstYearReg',  # Action for first-year regular student
    'property(pass_year)': '2025',  # Assuming the exam is for the year 2025
    'year': '1',  # Year of study is 1st year
    'category': 'R',  # Category for regular students
    'hallticket_no': '2561116713',  # The student ID you provided
}

# Send the POST request
response = requests.post(url, data=form_data)

# Check if the response was successful
if response.status_code == 200:
    # Parse the response with BeautifulSoup
    soup = BeautifulSoup(response.text, 'html.parser')

    # Print the raw HTML to check the structure of the result
    # You can comment this line out once you identify the correct result selector
    print(soup.prettify())

    # Example: Find the result (adjust this based on actual HTML structure)
    # You need to inspect the response and find the actual result location
    result = soup.find('div', class_='result')  # Adjust based on actual structure

    if result:
        print("Student Result:", result.text.strip())
    else:
        print("Result not found.")
else:
    print(f"Failed to retrieve the result. Status code: {response.status_code}")

i already have this. make ur changes in this

Edit
Looking at your code, it's trying to access the results from the official results page using a POST request. Let's make some changes based on the HTTP log you shared, which suggests a different endpoint structure might be in use.

Here's the modified code that uses the endpoint shown in your terminal screenshot:

python
import requests
from bs4 import BeautifulSoup

# Set the URL to the endpoint seen in the terminal logs
url = 'http://results.cgg.gov.in/tg_res/fetch-result.php'  # First year endpoint

# Set the form data based on what we know
form_data = {
    'hallticket_no': '2561116713',  # The student ID you provided
    'year': '1',  # 1 for first year
    'category': 'G',  # G for General (changed from 'R' which was for Regular)
    'pass_year': '2025'  # Exam year
}

# Add headers to mimic a browser request
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36',
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
    'Origin': 'http://results.cgg.gov.in',
    'Referer': 'http://results.cgg.gov.in/results.html'
}

# Send the POST request
try:
    response = requests.post(url, data=form_data, headers=headers)
    
    # Check if the response was successful
    if response.status_code == 200:
        # Try to parse as JSON first (common for API responses)
        try:
            result_data = response.json()
            print("Result Data (JSON):", result_data)
        except:
            # If not JSON, parse with BeautifulSoup
            soup = BeautifulSoup(response.text, 'html.parser')
            
            # Save the full HTML response to a file for inspection
            with open('result_response.html', 'w', encoding='utf-8') as f:
                f.write(soup.prettify())
            
            print("Raw response saved to 'result_response.html'")
            
            # Try to find common result elements
            # This is a guess - you'll need to adjust based on actual HTML structure
            result_table = soup.find('table', class_='marks_table_styles')
            if result_table:
                print("Found results table:")
                for row in result_table.find_all('tr'):
                    print(' | '.join([cell.text.strip() for cell in row.find_all(['td', 'th'])]))
            else:
                # Look for any result indicators
                result_div = soup.find(['div', 'section'], id=['result', 'studentResult', 'marks'])
                if result_div:
                    print("Result Information:", result_div.text.strip())
                else:
                    print("No specific result elements found. Check the saved HTML file.")
    else:
        print(f"Failed to retrieve the result. Status code: {response.status_code}")
        print("Response text:", response.text)

except Exception as e:
    print(f"An error occurred: {str(e)}")
Changes made:

Updated the URL to match the one shown in your terminal screenshot (/tg_res/fetch-result.php)
Changed category from 'R' to 'G' as the form in the HTML used 'G' for General
Added headers to make the request appear more like it's coming from a browser
Enhanced error handling and response processing:
Try to parse as JSON first (APIs often return JSON)
Save the raw HTML to a file for inspection
Try multiple approaches to extract result data
Provide more detailed error output
This code should give you a better starting point. You might need to:

Adjust the URL if the domain is different
Fine-tune the form parameters based on the actual requirements
Modify the HTML parsing once you see the actual structure of the response
If this doesn't work, examining the saved HTML file will help you understand what data is being returned and how to extract it.





PS C:\Sudheer\Py Playground> py index.py
An error occurred: HTTPConnectionPool(host='results.cgg.gov.in', port=80): Max retries exceeded with url: /tg_res/fetch-result.php (Caused by ConnectTimeoutError(<urllib3.connection.HTTPConnection object at 0x0000021894052120>, 'Connection to results.cgg.gov.in timed out. (connect timeout=None)'))
PS C:\Sudheer\Py Playground>

Edit
It looks like you're experiencing a connection timeout when trying to reach the server. This could be due to several reasons:

The server might be blocking requests that don't come from the official website
The URL could be incorrect or accessible only within certain networks
The server might be down or experiencing high traffic
Let's try a different approach:

python
import requests
from bs4 import BeautifulSoup
import time

# We'll try both the URL paths we've seen
urls = [
    'http://results.cgg.gov.in/bieresultliveNewChanges2025.do',  # Original URL from your code
    'http://results.cgg.gov.in/tg_res/fetch-result.php',         # URL from terminal screenshot
    'https://results.cgg.gov.in/bieresultliveNewChanges2025.do', # HTTPS version
    'https://results.cgg.gov.in/tg_res/fetch-result.php'         # HTTPS version
]

form_data = {
    'actionpart': 'getBieResultFirstYearGen',  # Changed to match the form's JavaScript
    'property(pass_year)': '2025',
    'year': '1', 
    'category': 'G',
    'property(month)': '3',  # From the form, this is for IPE exams
    'hallticket_no': '2561116713'
}

headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36',
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8'
}

# Try each URL with a short timeout
for url in urls:
    try:
        print(f"Trying URL: {url}")
        response = requests.post(url, data=form_data, headers=headers, timeout=10)
        
        print(f"Status code: {response.status_code}")
        if response.status_code == 200:
            # Save the response content to a file for inspection
            with open('result_response.html', 'w', encoding='utf-8') as f:
                f.write(response.text)
            
            print(f"Success! Response saved to 'result_response.html'")
            break  # Exit the loop if successful
    except Exception as e:
        print(f"Error with {url}: {str(e)}")
    
    print("Waiting 2 seconds before trying next URL...")
    time.sleep(2)
This script:

Tries multiple URL variations
Sets a 10-second timeout to avoid hanging
Uses the exact form parameters from the HTML form
Saves any successful response to a file
If all these URLs fail, there might be additional considerations:

The server might require specific cookies or session information
The site might use JavaScript to generate or modify form data before submission
There could be IP-based restrictions or rate limiting
In these cases, you might need to:

First visit the main page to get cookies
Use a tool like Selenium that can execute JavaScript
Look more closely at how the form is submitted in the actual website





check this out


<html lang="EN-IN" class="no-js"><head><meta charset="utf-8"><meta name="google-site-verification" content="UJ0Grhv9torX-u90bqOTwW3jrBhNlXalD1Ruc_WtFPM"><meta name="viewport" content="width=device-width, initial-scale=1.0"><meta name="robots" content="index, follow"><meta name="googlebot" content="i

pasted



<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"> <html> <head> <title>:: Memo Download ::::</title> <meta http-equiv="pragma" content="no-cache"> <meta http-equiv="cache-control" content="no-cache"> <meta http-equiv="expires" content="0"> <meta http-equiv="keywords" content="



Pasted content

61.86 KB •804 lines
•
Formatting may be inconsistent from source

<html lang="EN-IN" class="no-js"><head><meta charset="utf-8"><meta name="google-site-verification" content="UJ0Grhv9torX-u90bqOTwW3jrBhNlXalD1Ruc_WtFPM"><meta name="viewport" content="width=device-width, initial-scale=1.0"><meta name="robots" content="index, follow"><meta name="googlebot" content="index,follow"><meta name="googlebot-news" content="index, follow"><title>Telangana Inter 1st Year Result 2025 | TG Inter Results 2025 | TS Inter Results | తెలంగాణ ఇంటర్ ఫలితాలు 2025 - Eenadu</title><meta name="keywords" content="tg inter results 2025, inter results 2025, tg inter results 2025 telugu,ts inter results 2025 link download, ts inter results 2025, inter results 2025, ts inter results 2025 telugu, ts inter results date, tsbie results, inter 1st year results, ts inter 1st year results, ts inter results 2025 1st year, ts inter results 2025 tsbie, tsbie results 2025, inter results 2025 date telangana, when ts inter results 2025, when inter results 2025 ts, ts inter results 2025, india results ts inter 2025 1st year, ts inter results, ts intermediate 1st year results 2025, tg intermediate 1st year results 2025"><meta name="description" content="Telangana Inter 1st Year Result 2025 - As per official notification of Telangana Intermediate Board, Intermediate 1st year results will be released soon. Check your Inter 1st year result by entering your hall ticket number on the website results.eenadu.net"><meta name="news_keywords" content="tg inter results 2025, inter results 2025, tg inter results 2025 telugu,ts inter results 2025 link download, ts inter results 2025, inter results 2025, ts inter results 2025 telugu, ts inter results date, tsbie results, inter 1st year results, ts inter 1st year results, ts inter results 2025 1st year, ts inter results 2025 tsbie, tsbie results 2025, inter results 2025 date telangana, when ts inter results 2025, when inter results 2025 ts, ts inter results 2025, india results ts inter 2025 1st year, ts inter results, ts intermediate 1st year results 2025, tg intermediate 1st year results 2025"><meta name="abstract" content="Telangana Inter 1st Year Result 2025 - As per official notification of Telangana Intermediate Board, Intermediate 1st year results will be released soon. Check your Inter 1st year result by entering your hall ticket number on the website results.eenadu.net"><meta name="HandheldFriendly" content="true"><meta name="apple-touch-fullscreen" content="YES"><meta property="fb:app_id" content="2296212830610113"><meta property="fb:pages" content="282370161903806"><meta property="og:url" content="https://results.eenadu.net/tg-inter-2025/tg-inter-1st-year-results-general.aspx"><meta property="og:site_name" content="EENADU"><meta property="og:title" itemprop="name" content="తెలంగాణ ఇంటర్&zwnj; ప్రథమ సంవత్సరం ఫలితాలు"><meta property="og:description" itemprop="description" content="Telangana Intermediate 1st Year Result 2025"><meta property="og:image" itemprop="image" content="https://results.eenadu.net/tg-inter-2025/images/tg-inter.webp"><meta property="og:image:url" content="https://results.eenadu.net/tg-inter-2025/images/tg-inter.webp"><meta property="og:image" content="https://results.eenadu.net/tg-inter-2025/images/tg-inter.webp"><meta property="og:type" content="website"><meta property="og:image:type" content="image/jpeg"><meta property="og:image:width" content="680"><meta property="og:image:height" content="310"><meta property="og:imageWidth" content="680"><meta property="og:imageHeight" content="310"><link itemprop="image" href="https://results.eenadu.net/tg-inter-2025/images/tg-inter.webp"><meta name="twitter:card" content="summary_large_image"><meta name="twitter:site" content="@eenaduresults"><meta name="twitter:creator" content="@Eenadu.NET"><meta name="twitter:title" content="తెలంగాణ ఇంటర్&zwnj; ప్రథమ సంవత్సరం ఫలితాలు"><meta name="twitter:description" content="Telangana Intermediate 1st Year Result 2025"><meta name="twitter:image" content="https://results.eenadu.net/tg-inter-2025/images/tg-inter.webp"><meta itemprop="image" content="https://results.eenadu.net/tg-inter-2025/images/tg-inter.webp"><meta itemprop="author" content="EENADU"><meta itemprop="publisher" content="EENADU"><meta itemprop="headline" content="తెలంగాణ ఇంటర్&zwnj; ప్రథమ సంవత్సరం ఫలితాలు"><link rel="shortcut icon" type="image/x-icon" href="../favicon.ico"><link href="../css/reslt.css?v=16042025" rel="stylesheet" type="text/css"><link href="../css/reslt-new.css?v=16042025" rel="stylesheet" type="text/css"><link href="../css/header.css?v=16042025" rel="stylesheet" type="text/css"><link href="../UniFont/eenadu-webfont.css?v=16042025" rel="stylesheet" type="text/css">
    <script async="" src="https://sb.scorecardresearch.com/cs/20416623/beacon.js"></script><script async="" src="https://www.googletagmanager.com/gtm.js?id=GTM-NLSKVH9D"></script><script src="../js/jquery.min.js"></script>
   
 
    <!-- Google Tag Manager -->
<script>
    (function (w, d, s, l, i) {
        w[l] = w[l] || []; w[l].push({
            'gtm.start':
                new Date().getTime(), event: 'gtm.js'
        }); var f = d.getElementsByTagName(s)[0],
            j = d.createElement(s), dl = l != 'dataLayer' ? '&l=' + l : ''; j.async = true; j.src =
                'https://www.googletagmanager.com/gtm.js?id=' + i + dl; f.parentNode.insertBefore(j, f);
    })(window, document, 'script', 'dataLayer', 'GTM-NLSKVH9D');</script>
<!-- End Google Tag Manager -->
<!-- GA4 Results Site Tag -->
<script async="" src="https://www.googletagmanager.com/gtag/js?id=G-29V2PXW4CF"></script>
<script>
    window.dataLayer = window.dataLayer || [];
    function gtag() { dataLayer.push(arguments); }
    gtag('js', new Date());
    gtag('config', 'G-29V2PXW4CF', {
        'send_page_view': true
    });
</script>
<script>
    function gtagEvent(eventcategory, eventlabel, action) {
        if (gtag) {
            gtag('event', action, {
                'send_to': 'G-29V2PXW4CF',
                'event_category': eventcategory,
                'event_label': eventlabel
            });

        }
    }
</script>
<!-- Start Comscore Tag -->
<script>
    var _comscore = _comscore || [];
    _comscore.push({
        c1: "2", c2: "20416623",
        options: {
            enableFirstPartyCookie: true,
            bypassUserConsentRequirementFor1PCookie: true
        }
    });

    (function () {
        var s = document.createElement("script"), el = document.getElementsByTagName("script")[0]; s.async = true;
        s.src = "https://sb.scorecardresearch.com/cs/20416623/beacon.js";
        el.parentNode.insertBefore(s, el);
    })();
</script>
<noscript>
    <img src="https://sb.scorecardresearch.com/p?c1=2&c2=20416623&cv=4.4.0&cj=1">
</noscript>
<!-- End Comscore Tag -->
<style>
/*html{box-sizing:border-box}*,*::before,*::after{box-sizing:inherit;padding:0;margin:0}
body{font-family:-apple-system,BlinkMacSystemFont,San Francisco,Helvetica Neue,Helvetica,Ubuntu,Roboto,Noto,Segoe UI,Arial,sans-serif}*/
.hidden{display:none}svg{width:20px;height:20px;margin-right:7px}
.share-button,.copy-link{padding-left:30px;padding-right:30px}
.share-button,.share-dialog{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%)}
.share-dialog{display:none;width:95%;max-width:500px;box-shadow:0 8px 16px rgba(0,0,0,.15);z-index:-1;border:1px solid #ddd;padding:20px;border-radius:4px;background-color:#fff}
.share-dialog.is-open{display:block;z-index:2}
.targets{display:grid;grid-template-rows:1fr 1fr;grid-template-columns:1fr 1fr;grid-gap:20px;margin-bottom:20px}
.close-button{background-color:transparent;border:0;padding:0}
.close-button svg{margin-right:0}
.pen-url{margin-right:15px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
</style>
</head>
<body>

<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-NLSKVH9D"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
               
    <div id="wrapper">
        <!-- road block body advt starts -->
        <!--<div id="body_ad">
    <div id="right-nt">
        <div id="902aa6a7-e116-41c8-9358-863df5b4c4f4" class="_ap_apex_ad">
            <script>
                var adpushup = window.adpushup = window.adpushup || {};
                adpushup.que = adpushup.que || [];
                adpushup.que.push(function () {
                    adpushup.triggerAd("902aa6a7-e116-41c8-9358-863df5b4c4f4");
                });</script>
        </div>
    </div>
    <div id="left-nt">
        <div id="3b7e71e7-9cad-4af8-ac4e-1d401e95d23f" class="_ap_apex_ad">
            <script>
                    var adpushup = window.adpushup = window.adpushup || {};
                    adpushup.que = adpushup.que || [];
                    adpushup.que.push(function () {
                        adpushup.triggerAd("3b7e71e7-9cad-4af8-ac4e-1d401e95d23f");
                    });</script>
        </div>
    </div>
</div>-->
       
<div id="body_ad">
    <div id="right-nt">
        <a href="https://admission.sathyabama.ac.in/?utm_source=Eenadu&amp;utm_medium=12th_result_page&amp;utm_campaign=Direct_Admission2025" target="_blank">
            <img src="ads/Sathyabama/Sathyabama-University-Results-120X600.jpg" alt="advertisement" onclick="gtagEvent('tg_inter_results_2025', 'Sathyabama', 'TG-Inter I-Right-120x600-Sathyabama');">
        </a>
    </div>
    <div id="left-nt">
        <a href="https://admission.sathyabama.ac.in/?utm_source=Eenadu&amp;utm_medium=12th_result_page&amp;utm_campaign=Direct_Admission2025" target="_blank">
            <img src="ads/Sathyabama/Sathyabama-University-Results-120X600.jpg" alt="advertisement" onclick="gtagEvent('tg_inter_results_2025', 'Sathyabama', 'TG-Inter I-Left-120x600-Sathyabama');">
        </a>
    </div>
</div>


        <!-- road block body advt ends -->

        <!-- -----header starts----------- -->
        <header style="background-color: #FFF; display: block;" class="desktop-header">
            <div class="topnav1">
                <div class="etop-right"><span class="ep1"><a href="https://www.eenadu.net/feedback" target="_blank" title="eenadu feedback">Feedback</a> | <a href="https://epaper.eenadu.net/" target="_blank" title="eenadu e-paper">E-PAPER</a> | <a href="https://pratibha.eenadu.net/" target="_blank" title="ETV BHARAT Telugu">Pratibha</a></span></div>
            </div>
            <!-- top-nav ends here -->

            <div>
               <figure class="logo">
                    <a href="https://www.eenadu.net/">
                        <img src="../images/logo.webp" alt="Eenadu.net Logo" width="268" height="66"></a>
                    <figcaption></figcaption>
                </figure>
                <!-- logo class ends -->
                <!--<div class="ad728-top-nt">
    <div id="6641c1e0-a508-4b12-ab63-1270704e9b94" class="_ap_apex_ad">
        <script>
                    var adpushup = window.adpushup = window.adpushup || {};
                    adpushup.que = adpushup.que || [];
                    adpushup.que.push(function () {
                        adpushup.triggerAd("6641c1e0-a508-4b12-ab63-1270704e9b94");
                    });</script>
    </div>
</div>-->
<div class="ad728-top-nt">
    <a href="https://admission.sathyabama.ac.in/?utm_source=Eenadu&amp;utm_medium=12th_result_page&amp;utm_campaign=Direct_Admission2025" target="_blank">
        <img src="ads/Sathyabama/Sathyabama-University-Results-728X90.jpg" alt="advertisement" onclick="gtagEvent('tg_inter_results_2025', 'Sathyabama', 'TG-Inter I-728x90-Sathyabama');">
    </a>
</div>

            </div>
            <div class="clearfix"></div>
            <!-- Menu Starts -->
            <nav class="spmenu" id="navbar">
    <ul>
        <li class="left no-border"><span id="lblDateTime">మంగళవారం, ఏప్రిల్ 22, 2025</span></li>
        <li class="no-border right sp-srch"><a href="https://www.eenadu.net/search" target="_blank" aria-label="Eenadu Search"><span class="sp-srch-ico"></span></a></li>
        <li class="no-border right "><a href="https://www.eenadu.net/" class="special-e-home">ఈనాడు హోం</a></li>
        <li class="no-border right"><a href="/" class="special-pg-home">హోం</a></li>
    </ul>
</nav>
            <!-- Menu ends -->
        </header>
        <div class="clearfix"></div>
        <!-- -----header ends----------- -->
        <!-- mobile -->
        <div class="mobile-header">
    <div class="header">
        <div class="nav-top">
            <div class="side-nav-bar sd-nav-bar" style="display: block;" id="mySidebar">
                <button type="button" role="button" onclick="w3_close()" class="w3-bar-item w3-large"> ×</button>
                <!-- <div class="aside-backdrop" onclick="w3_close()"></div> -->
                <div class="navbar">
                    <ul id="myDIV">
                        <li class="home-img"><a href="https://www.eenadu.net/" class="n-btn active"></a></li>
                        <li class="dropdown">
                            <button type="button" role="button" class="dropbtn n-btn cl-btn nv-second">ఆంధ్రప్రదేశ్  <i>▼</i></button>
                            <div class="dropdown-content sec-drop div-con-drop">
                                <ul>
                                    <li><a href="https://www.eenadu.net/andhra-pradesh" class="n-btn">రాష్ట్ర వార్తలు</a></li>
                                    <li><a href="https://www.eenadu.net/andhra-pradesh/districts" class="n-btn">జిల్లా వార్తలు</a></li>
                                </ul>
                            </div>
                        </li>
                        <li class="dropdown">
                            <button type="button" role="button" class="dropbtn n-btn cl-btn nv-third">తెలంగాణ  <i>▼</i></button>
                            <div class="dropdown-content thr-drop div-con-drop">
                                <ul>
                                    <li><a href="https://www.eenadu.net/telangana" class="n-btn">రాష్ట్ర వార్తలు</a></li>
                                    <li><a href="https://www.eenadu.net/telangana/districts" class="n-btn">జిల్లా వార్తలు</a></li>
                                </ul>
                            </div>
                        </li>
                        <!-- <li><a href="#" class="n-btn"> ఆంధ్రప్రదేశ్ </a></li> -->
                        <!-- <li><a href="#" class="n-btn">  తెలంగాణ </a></li> -->
                        <li><a href="https://www.eenadu.net/india" class="n-btn"> జాతీయం </a></li>
                        <li><a href="https://www.eenadu.net/world" class="n-btn"> అంతర్జాతీయం </a></li>
                        <li><a href="https://www.eenadu.net/crime" class="n-btn"> క్రైమ్  </a></li>
                        <!-- <li><a href="https://www.eenadu.net/politics" class="n-btn"> పాలిటిక్స్  </a></li>-->
                        <li><a href="https://www.eenadu.net/business" class="n-btn"> బిజినెస్ </a></li>
                        <li><a href="https://www.eenadu.net/sports" class="n-btn">  క్రీడలు  </a></li>
                        <li><a href="https://www.eenadu.net/movies" class="n-btn"> సినిమా </a></li>
                        <li class="dropdown">
                            <button type="button" role="button" class="dropbtn n-btn cl-btn nv-first">ఫీచర్ పేజీలు  <i>▼</i></button>
                            <div class="dropdown-content first-drop div-con-drop">
                                <ul>
                                    <li><a href="https://www.eenadu.net/women" class="n-btn">వసుంధర</a></li>
                                    <li><a href="https://www.eenadu.net/education" class="n-btn">చదువు</a></li>
                                    <li><a href="https://www.eenadu.net/health" class="n-btn">సుఖీభవ</a></li>
                                    <li><a href="https://www.eenadu.net/technology" class="n-btn">ఈ-నాడు</a></li>
                                    <li><a href="https://www.eenadu.net/devotional" class="n-btn">మకరందం</a></li>
                                    <li><a href="https://www.eenadu.net/youth" class="n-btn">ఈ తరం</a></li>
                                    <li><a href="https://www.eenadu.net/recipes" class="n-btn">ఆహా</a></li>
                                    <li><a href="https://www.eenadu.net/kids-stories" class="n-btn">హాయ్ బుజ్జీ</a></li>
                                    <li><a href="https://www.eenadu.net/real-estate" class="n-btn">స్థిరాస్తి</a></li>
                                    <li><a href="https://www.eenadu.net/temples" class="n-btn">దేవతార్చన</a></li>
                                    <li><a href="https://stories.eenadu.net" class="n-btn">వెబ్&zwnj; స్టోరీస్&zwnj;</a></li>
                                    <li><a href="https://www.eenadu.net/viral-videos" class="n-btn">వైరల్ వీడియోస్ </a></li>
                                    <li><a href="https://www.eenadu.net/kathalu" class="n-btn">కథామృతం</a></li>
                                </ul>
                            </div>
                        </li>
                        <li><a href="https://www.eenadu.net/photos" class="n-btn"> ఫొటోలు </a></li>
                        <li><a href="https://www.eenadu.net/videos" class="n-btn">  వీడియోలు   </a></li>
                        <li><a href="https://www.eenadu.net/nri" class="n-btn"> ఎన్ఆర్ఐ </a></li>
                        <li><a href="https://www.eenadu.net/explained" class="n-btn"> వెబ్ ప్రత్యేకం </a></li>
                        <!-- <li><a href="#" class="n-btn">  పాంచ్ పటాకా   </a></li> -->
                        <li><a href="https://www.eenadu.net/sunday-magazine" class="n-btn"> సండే మ్యాగజైన్ </a></li>
                        <li><a href="https://www.eenadu.net/agriculture" class="n-btn"> అన్నదాత </a></li>
                        <li><a href="https://www.eenadu.net/calendar" class="n-btn">  క్యాలెండర్   </a></li>
                        <li><a href="http://results.eenadu.net" class="n-btn"> రిజల్ట్స్ </a></li>
                    </ul>
                    <ul class="nav-social">
                        <li><a href="https://epaper.eenadu.net">E-Paper</a></li>
                        <li><a href="https://www.eenadu.net/archives/home">Archives</a></li>
                        <li><a href="https://www.eenadu.net/terms-conditions">Terms &amp; Conditions</a></li>
                        <li><a href="https://www.eenadu.net/privacy-policy">Privacy Policy</a></li>
                    </ul><!--nav-social-->

                    <ul class="nav-soc-icon">
                        <li><a href="https://www.facebook.com/eenaduonline" aria-label="Eenadu Facebook"><img loading="lazy" src="https://assets.eenadu.net/_assets/_images/social-icons-facebook.webp" alt="Eenadu Facebook" width="27" height="27"></a></li>
                        <li><a href="https://twitter.com/eenadulivenews" aria-label="Eenadu Twitter"><img loading="lazy" src="https://assets.eenadu.net/_assets/_images/social-icons-twitter.webp" alt="Eenadu Twitter" width="27" height="27"></a></li>
                        <li><a href="https://www.instagram.com/eenadulivenews/?hl=en" aria-label="Eenadu Instagram"><img loading="lazy" src="https://assets.eenadu.net/_assets/_images/social-icons-instagram.webp" alt="Eenadu Instagram" width="27" height="27"></a></li>
                        <!-- <li><a href="#"><img loading="lazy" src="images/social-icons-telegram.png" alt="Eenadu Telegram" width="27" height="27"></a></li> -->
                        <li><a href="https://news.google.com/s/CBIwsNmunUE?r=7&amp;oc=1" aria-label="Eenadu Google News"><img loading="lazy" src="https://assets.eenadu.net/_assets/_images/social-icons-google-news.webp" alt="Eenadu Google News" width="27" height="27"></a></li>
                        <!-- <li><a href="https://sharechat.com/profile/eenadulivenews"><img loading="lazy" src="https://assets.eenadu.net/_assets/_images/social-icons-sharechat.png" alt="Eenadu Sharechat" width="27" height="27"></a></li> -->
                        <!-- <li><a href="https://www.kooapp.com/profile/eenadulivenews"><img loading="lazy" src="https://assets.eenadu.net/_assets/_images/social-icons-kooapp.png" alt="Eenadu Koo" width="27" height="27"></a></li> -->
                        <li><a href="#" aria-label="Eenadu youtube"><img loading="lazy" src="https://assets.eenadu.net/_assets/_images/social-icons-youtube.webp" alt="Eenadu youtube" width="27" height="27"></a></li>

                    </ul>
                </div><!--navbar-->
            </div><!--side-nav-bar-->
            <!-- Page Content -->
            <div class="nav-2 sd-nav-2">
                <a href="https://www.eenadu.net/"><img src="https://assets.eenadu.net/_assets/amp/imgs/mb-logo.webp" width="256" height="40" alt="logo"></a>
                <!-- <span>గురువారం, ఆగస్టు 19, 2021</span> -->
            </div><!--nav-2-->
            <div class="nav-4 sd-nav-4">
                <a href="https://whatsapp.com/channel/0029Va9Qnis6BIEcfIyieG0r" name="trending"><span class="whatsapp-join-icon"><p class="wh-cnl">Channel</p></span></a>
            </div>
            <div class="nav-3 sd-nav-3">
                <a href="https://www.eenadu.net/search" aria-label="search"><span class="Search-img"></span></a>
            </div><!--nav-3-->
            <div class="nav-5 sd-nav-5">
                <a href="https://www.eenadu.net/breaking-news-list" aria-label="bellicon"><span class="bell-icon"></span></a>
            </div><!--nav-5-->
            <div class="nav-1 sd-nav-1"><button type="button" role="button" class="nav-btn" onclick="w3_open()" aria-label="Eenadu Mobile Menu">☰</button></div><!--nav-1-->
            <!--nav-1-->
        </div><!--nav-top-->
    </div><!--header-->

    <div class="fs-header-2 hedstick" id="nav-bottom">
        <div class="fs-nav">
            <a href="https://results.eenadu.net/">హోం</a>
            <a href="https://www.eenadu.net/">ఈనాడు హోం</a>
        </div><!--fs-nav-->
        <!--<div class="fs-search">
            <form class="srch-blue hmsearch">
               
                <a href="https://www.eenadu.net/search" target="_blank">
                    <div class="search-blue"></div>
                </a>
            </form>
        </div>--><!--fs-search-->
    </div><!--fs-header-2-->
</div>

       
        <div class="clearfix"></div>
        <!-- Header Part End -->
        <!-- Top Ads Section Start -->
        <section class="offset-t">
            <!-- include file = ads/1st-Year/d_top_460x120.htm -->
            <div class="clearfix"></div>
        </section>
        <!-- Top Ads Section End -->
         
        <!-- 3 column Section Start -->
         <form method="post" action="./tg-inter-1st-year-results-general.aspx" onsubmit="javascript:return WebForm_OnSubmit();" id="form1">
<div class="aspNetHidden">




</div>

<script type="text/javascript">
//<![CDATA[
var theForm = document.forms['form1'];
if (!theForm) {
    theForm = document.form1;
}
function __doPostBack(eventTarget, eventArgument) {
    if (!theForm.onsubmit || (theForm.onsubmit() != false)) {
        theForm.__EVENTTARGET.value = eventTarget;
        theForm.__EVENTARGUMENT.value = eventArgument;
        theForm.submit();
    }
}
//]]>
</script>


<script src="/WebResource.axd?d=U1JRQqdICgwDp3BFLVnaHlfpJv1uYJlsLpl1ayOH5hrSo48End4WZkkohWFspMvDzC8drOrM8XTmYzeIyfh6BdYioiE1&amp;t=637814653746327080" type="text/javascript"></script>


<script src="/ScriptResource.axd?d=NENNOlF6NaeBw9z9omcpPVWkDM7kX9pDPh0V_j0VgzbM6y1E8DC9a0xlTaRIBMcewRElaKvktV0ON3AjFYVYvFPQyi-sOQWuPUKuctEwLYPt92ia6Q4XPycahpJyNY0MPEtP6TjtHI4XKxXgq4QIkGVVI4c1&amp;t=14d69f50" type="text/javascript"></script>
<script src="/ScriptResource.axd?d=JiM4pDl9mkMcW7K8dIXs6Qc4OFCVwEQ7o9g9U7iCM9AM6wNwbdpzCblLKDp2bTjnfHahRim2Az68OVVcOIcY5AswWnszQ1Oid6lF_yHLPaxOXKr5YxhAqg39hGQxxcXkMepmAAtPQUaI4vNG_aKTLwLXOOskr9ZGUZPBpDoKKWAQdpjQ0&amp;t=49337fe8" type="text/javascript"></script>
<script src="/ScriptResource.axd?d=faxQB1lGxMbFMPEIGnagV78XoMPmjgzmXErGjHVuZgTt-gClJf3qGtTpy8xOCv_Qzh-o4WK408a2AuqwHKY7JPWYv14HoQSCFiZtXWaAz-f6IiPW0R7LlIpkIQWrCk52lbN6-hD6B3Al5MjyufWFUcseeHAKbkyLZlV4xy9YFXjVVz-00&amp;t=49337fe8" type="text/javascript"></script>
<script src="/WebResource.axd?d=_kdYz8ugndgWO6WUpnhxG7HNkQJWNgRotzC1D8DMu0zdZN28AWlJOW9_nPWY9-yuAWerdSP7cj00_RYjMDvFcPbDo0E1&amp;t=637814653746327080" type="text/javascript"></script>
<script type="text/javascript">
//<![CDATA[
function WebForm_OnSubmit() {
if (typeof(ValidatorOnSubmit) == "function" && ValidatorOnSubmit() == false) return false;
return true;
}
//]]>
</script>

<div class="aspNetHidden">

	
	
	
	
</div>
        <section class="3col">
            <!-- include file = ads/1st-Year/d_left_160x160.htm -->
            <!---ad320 start---->
            <!--<div class="ad320">
    <div id="1551cfb4-0b9c-4ba4-828d-2d3f682def87" class="_ap_apex_ad">
        <script>
    var adpushup = window.adpushup = window.adpushup || {};
            adpushup.que = adpushup.que || [];
            adpushup.que.push(function () {
                adpushup.triggerAd("1551cfb4-0b9c-4ba4-828d-2d3f682def87");
            });</script>
    </div>
</div>-->

<ul class="ad300-s adshuf1">
    <li>
        <a href="https://admission.sathyabama.ac.in/?utm_source=Eenadu&amp;utm_medium=12th_result_page&amp;utm_campaign=Direct_Admission2025" target="_blank">
            <img src="ads/Sathyabama/Sathyabama-University-Results-300X250.jpg" alt="advertisement" onclick="gtagEvent('tg_inter_results_2025', 'Sathyabama', 'TG-Inter I-300x250-Sathyabama');">
        </a>
    </li>
  
   
  
</ul>





            <!---ad320 End----->
            <!-- Result Section Start -->
            
                <script type="text/javascript">
//<![CDATA[
Sys.WebForms.PageRequestManager._initialize('ScriptManager1', 'form1', ['tUpdatePanel1','UpdatePanel1'], [], [], 90, '');
//]]>
</script>

           <div id="UpdatePanel1">
                        <div class="resultscnt">

                            <!-- SOCILA SHARE ICON START -->
                            
<div class="sshare-c" style="margin-bottom:5px; display:block; float:right;">    
        <div class="fb-c"><a href="javascript: void(0);" onclick="javascript:window.open('https://www.facebook.com/sharer/sharer.php?u=https://results.eenadu.net/tg-inter-2025/tg-inter-1st-year-results-general.aspx&amp;title=Telangana first year results 2025: తెలంగాణ ఇంటర్&zwnj; ప్రథమ సంవత్సరం ఫలితాలు', '_blank','', 'menubar=no,toolbar=no,resizable=yes,scrollbars=yes,height=600,width=600');return false;" class="fb-ci" aria-label="Eenadu Facebook"></a></div>
        <div class="twt-c"><a href="https://twitter.com/intent/tweet?url=https://results.eenadu.net/tg-inter-2025/tg-inter-1st-year-results-general.aspx&amp;text=తెలంగాణ ఇంటర్&zwnj; ప్రథమ సంవత్సరం ఫలితాలు &amp;via=eenadulivenews" onclick="javascript:window.open(this.href, '_blank','', 'menubar=no,toolbar=no,resizable=yes,scrollbars=yes,height=600,width=600');return false;" class="twt-ci" aria-label="Eenadu Twitter"></a></div>
        <div class="whats-c"><a href="https://api.whatsapp.com/send?text=తెలంగాణ ఇంటర్&zwnj; ప్రథమ సంవత్సరం ఫలితాలు - https://results.eenadu.net/tg-inter-2025/tg-inter-1st-year-results-general.aspx" onclick="javascript:window.open(this.href, '_blank','', 'menubar=no,toolbar=no,resizable=yes,scrollbars=yes,height=600,width=600');return false;" class="whats-ci" aria-label="Eenadu whatsapp"></a></div>
        <div class="lnk-c"><a href="https://results.eenadu.net/tg-inter-2025/tg-inter-1st-year-results-general.aspx" class="lnk-ci" aria-label="Eenadu Link"></a></div>
        <span id="test" style="line-height: 30px;"></span>
        <!--<div class="socico-share"><a class="socico-share-icon f-soc"></a></div>-->
   
    <script>
        $('.lnk-ci').click(function (e) {
            e.preventDefault();
            debugger;
            var copyText = $(this).attr('href');
            document.addEventListener('copy', function (e) {
                e.clipboardData.setData('text/plain', copyText);
                e.preventDefault();
            }, true);
            document.execCommand('copy');
            $('#test').css('color', 'red');
            $('#test').append("Link Copied");
        });
    </script>
</div>
                            <div class="clearfix"></div>
                            <!-- SOCILA SHARE ICON END --> 

            <!-- mobile-heading-scl-icon -->
            <div class="hdr-in">
              <h1 class="eng-title">TG Intermediate Public Examinations I Year (General) 2025 Results</h1>
              <!-- SOCILA SHARE ICON START -->
                <div class="share-dialog">
    <header>
        <p class="dialog-title">Share this pen</p>
        <button class="close-button"><svg><use href="#close"></use></svg></button>
    </header>
    <div class="targets">
        <a class="button">
            <svg>
                <use href="#facebook"></use>
            </svg>
            <span>Facebook</span>
        </a>

        <a class="button">
            <svg>
                <use href="#twitter"></use>
            </svg>
            <span>Twitter</span>
        </a>

        <a class="button">
            <svg>
                <use href="#linkedin"></use>
            </svg>
            <span>LinkedIn</span>
        </a>

        <a class="button">
            <svg>
                <use href="#email"></use>
            </svg>
            <span>Email</span>
        </a>
    </div>
    <div class="link">
        <div class="pen-url">https://results.eenadu.net/tg-inter-2025/tg-inter-1st-year-results-general.aspx</div>
        <button class="copy-link">Copy Link</button>
    </div>
</div>
<div class="sshare-c scl-in" style="margin-bottom: 5px;display:block;float:right;">
    <div class="socico-share"><a class="socico-share-icon f-soc" aria-label="Eenadu Social Share"></a></div>
</div>
<svg class="hidden">
    <defs>
        <symbol id="share-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-share"><path d="M4 12v8a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-8"></path><polyline points="16 6 12 2 8 6"></polyline><line x1="12" y1="2" x2="12" y2="15"></line></symbol>

        <symbol id="facebook" viewBox="0 0 24 24" fill="#3b5998" stroke="#3b5998" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-facebook"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path></symbol>

        <symbol id="twitter" viewBox="0 0 24 24" fill="#1da1f2" stroke="#1da1f2" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-twitter"><path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"></path></symbol>

        <symbol id="email" viewBox="0 0 24 24" fill="#777" stroke="#fafafa" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-mail"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path><polyline points="22,6 12,13 2,6"></polyline></symbol>

        <symbol id="linkedin" viewBox="0 0 24 24" fill="#0077B5" stroke="#0077B5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-linkedin"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect x="2" y="9" width="4" height="12"></rect><circle cx="4" cy="4" r="2"></circle></symbol>

        <symbol id="close" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-x-square"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect><line x1="9" y1="9" x2="15" y2="15"></line><line x1="15" y1="9" x2="9" y2="15"></line></symbol>
    </defs>
</svg>
<!-- Footer End -->
<script>
    const shareButton = document.querySelector('.socico-share');
    const shareDialog = document.querySelector('.share-dialog');
    const closeButton = document.querySelector('.close-button');

    shareButton.addEventListener('click', event => {
        if (navigator.share) {
            navigator.share({
                title: 'TELANGANA INTER FIRST YEAR 2025 RESULTS',
                url: 'https://results.eenadu.net/tg-inter-2025/tg-inter-1st-year-results-general.aspx'
            }).then(() => {
                console.log('Thanks for sharing!');
            })
                .catch(console.error);
        } else {
            shareDialog.classList.add('is-open');
        }
    });

    closeButton.addEventListener('click', event => {
        shareDialog.classList.remove('is-open');
    });
</script>
                <div class="clearfix"></div>
              <!-- SOCILA SHARE ICON END -->
            </div>
                            <!-- Result display Block Start -->

                            <div class="cntblock" style="display: block;">
                                <div class="ht">
                                    <div class="hall">
                                        <label>Hall Ticket</label>
                                        <input name="txtHTNo" type="text" maxlength="10" id="txtHTNo" class="iht" placeholder="Enter Hall ticket">
                                        <input name="state" type="hidden" id="state" class="iht" value="AP">
                                        <input name="restype" type="hidden" id="restype" class="iht" value="INTER1">
                                    </div>
                                    <input type="submit" name="btnsubmitresults" value="Submit" onclick="javascript:WebForm_DoPostBackWithOptions(new WebForm_PostBackOptions(&quot;btnsubmitresults&quot;, &quot;&quot;, true, &quot;&quot;, &quot;&quot;, false, false))" id="btnsubmitresults" class="rsbt">
                                    <div class="rsbt2" onclick="window.print()" onclientclick="return validate()">Print</div>
                                </div>
                                <div class="clearfix"></div>

                                <div id="resultdiv">
                                    <div class="errorht">
                                        <span id="RegularExpressionValidator1" style="visibility:hidden;">Please enter Number</span>


                                        <span id="vreValidator" style="visibility:hidden;">Please enter 10 digit Hall Ticket No.</span>

                                        <span id="vrfValidator" style="visibility:hidden;">Please enter 10 digit Hall Ticket No.</span>

                                        <span id="lblStatus"></span>
                                    </div>

                                    <div class="row">
                                        <p>Hall Ticket No</p>
                                        <div class="stly1"><span>
                                            <span id="lblHTNo">2561116713</span></span></div>
                                    </div>
                                    <div class="row no-space-r">
                                        <p>Total</p>
                                        <div class="stly2"><span>
                                            <span id="lblTotal">465</span></span></div>
                                    </div>
                                    <div class="row">
                                        <p>Name</p>
                                        <div class="stly1"><span>
                                            <span id="lblName">CHEEDELLA LAKSHMI NAVYA MANASW</span></span></div>
                                    </div>
                                    <div class="row no-space-r">
                                        <p>Result / Grade</p>
                                        <div class="stly2"><span>
                                            <span id="lblResultGrade">A     </span></span></div>
                                    </div>
                                    <div class="clearfix"></div>
                                    <!-- First Yr Start -->
                                    <div class="first-year">
                                        <div class="subject1">
                                            <div class="ftitle">Subject</div>
                                            <div class="frow">
                                                <span id="lblSubName1"> ENGLISH</span></div>
                                            <div class="frow">
                                                <span id="lblSubName2"> SANSKRIT</span></div>
                                            <div class="frow">
                                                <span id="lblSubName3">MATHEMATICS  IA</span></div>
                                            <div class="frow">
                                                <span id="lblSubName4">MATHEMATICS  IB</span></div>
                                            <div class="frow">
                                                <span id="lblSubName5">PHYSICS</span></div>
                                            <div class="frow">
                                                <span id="lblSubName6">CHEMISTRY</span></div>
                                              <div class="frow">
                                                <span id="lblSubName7"> ENGLISH PRACTICALS</span></div>
                                        </div>
                                        <div class="marks1">
                                            <div class="ftitle">Marks</div>
                                            <div class="frow">
                                                <span id="lblSubMarks1"> 76 P</span></div>
                                            <div class="frow">
                                                <span id="lblSubMarks2"> 99 P</span></div>
                                            <div class="frow">
                                                <span id="lblSubMarks3"> 75 P</span></div>
                                            <div class="frow">
                                                <span id="lblSubMarks4"> 75 P</span></div>
                                            <div class="frow">
                                                <span id="lblSubMarks5"> 60 P</span></div>
                                            <div class="frow">
                                                <span id="lblSubMarks6"> 60 P</span></div>
                                              <div class="frow">
                                                <span id="lblSubMarks7"> 20 P</span></div>
                                        </div>
                                        <div class="clearfix"></div>
                                    </div>
                                    <!-- First Yr End -->
                                </div>

                            </div>

                            <!-- Result display Block end -->
                            <!-- Comming Soon display Block Start -->
                            <div class="soon" style="display: none !important;">Telangana Inter 1st Year Result 2025 will be Available Soon</div>
                            <!-- Comming Soon display Block end -->
                            <!-- 320 ad start -->
                            <!---ad320 start---->
            <!--<div class="ad320">
    <div id="7837c83f-12ab-4647-bf22-9fa0f40cc4a3" class="_ap_apex_ad">
        <script>var adpushup = window.adpushup = window.adpushup || {};
		adpushup.que = adpushup.que || [];
		adpushup.que.push(function() {
            adpushup.triggerAd("7837c83f-12ab-4647-bf22-9fa0f40cc4a3");
		});</script>
    </div>
</div>-->
<ul class="ad300-s adshuf1">
    <li>
        <a href="https://admissions.mallareddyuniversity.ac.in/?utm_source=Eenadu&amp;utm_medium=Display&amp;utm_campaign=Results" target="_blank">
            <img src="ads/MallaReddy/Malla_Reddy_University_300x250.jpg" alt="advertisement" onclick="gtagEvent('tg_inter_results_2025', 'MallaReddy', 'TG-Inter I-300x250-MallaReddy');">
        </a>
    </li>
</ul>


            <!---ad320 End----->
                               <div class="clearfix"></div>
                            <!-- 320 ad End -->
                            <!--<div class="add728">  
    <div id="bc80ec37-7a2f-4c3f-8b11-5f9a2fbe069e" class="_ap_apex_ad">
        <script>var adpushup = window.adpushup = window.adpushup || {};
		adpushup.que = adpushup.que || [];
		adpushup.que.push(function() {
            adpushup.triggerAd("bc80ec37-7a2f-4c3f-8b11-5f9a2fbe069e");
		});</script>
    </div>  
</div>-->

<div class="add728">
    <a href="https://admissions.mallareddyuniversity.ac.in/?utm_source=Eenadu&amp;utm_medium=Display&amp;utm_campaign=Results" target="_blank">
        <img src="ads/MallaReddy/Malla_Reddy_University_728X90.jpg" alt="advertisement" onclick="gtagEvent('tg_inter_results_2025', 'MallaReddy', 'TG-Inter I-728x90-MallaReddy');">
    </a>
</div>
                            <!-- Other Link start -->
                            <div class="lnk"><a href="tg-inter-1st-year-results-vocational.aspx">Click Here Telangana Intermediate I Year (Vocational) 2025 Results</a></div>
                            <!-- Other Link end -->
                            <!-- Info start -->
                             <div class="info" style="display:none;">
                                <p>
                                    P - PASS, *P - SUPPLEMENTARY PASS, F - FAIL, *F - SUPPLEMENTARY FAIL A - ABSENT,
                                    W - WITHHELD, M - MALPRACTICE, N - NOT REGISTERED<br>
                                    <span>Grade A</span>: Greater Than or Equal to 75%
                                    <br>
                                    <span>Grade B</span>: Greater Than or Equal to 60% And Less than 75%<br>
                                    <span>Grade C</span>: Greater Than or Equal to 50% And Less than 60%
                                    <br>
                                    <span>Grade D</span>: Greater Than or Equal to 35% And Less than 50%
                                </p>
                            </div>
                            <!-- Info End -->
                            <div class="clearfix"></div>
                             <br>
                             <!-- include file = ads/ep-links.htm -->
                        </div>
                   </div>
                  
            
            <!-- Result Section End -->
            <!-- include file = ads/1st-Year/d_right_160x160.htm -->

            <div class="clearfix"></div>
            
        </section>
              
<script type="text/javascript">
//<![CDATA[
var Page_Validators =  new Array(document.getElementById("RegularExpressionValidator1"), document.getElementById("vreValidator"), document.getElementById("vrfValidator"));
//]]>
</script>

<script type="text/javascript">
//<![CDATA[
var RegularExpressionValidator1 = document.all ? document.all["RegularExpressionValidator1"] : document.getElementById("RegularExpressionValidator1");
RegularExpressionValidator1.controltovalidate = "txtHTNo";
RegularExpressionValidator1.focusOnError = "t";
RegularExpressionValidator1.errormessage = "Please enter Number";
RegularExpressionValidator1.evaluationfunction = "RegularExpressionValidatorEvaluateIsValid";
RegularExpressionValidator1.validationexpression = "^\\d+$";
var vreValidator = document.all ? document.all["vreValidator"] : document.getElementById("vreValidator");
vreValidator.controltovalidate = "txtHTNo";
vreValidator.focusOnError = "t";
vreValidator.errormessage = "Please enter 10 digit Hall Ticket No.";
vreValidator.evaluationfunction = "RegularExpressionValidatorEvaluateIsValid";
vreValidator.validationexpression = "[0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9]";
var vrfValidator = document.all ? document.all["vrfValidator"] : document.getElementById("vrfValidator");
vrfValidator.controltovalidate = "txtHTNo";
vrfValidator.errormessage = "Please enter 10 digit Hall Ticket No.";
vrfValidator.evaluationfunction = "RequiredFieldValidatorEvaluateIsValid";
vrfValidator.initialvalue = "";
//]]>
</script>


<script type="text/javascript">
//<![CDATA[

var Page_ValidationActive = false;
if (typeof(ValidatorOnLoad) == "function") {
    ValidatorOnLoad();
}

function ValidatorOnSubmit() {
    if (Page_ValidationActive) {
        return ValidatorCommonOnSubmit();
    }
    else {
        return true;
    }
}
        
theForm.oldSubmit = theForm.submit;
theForm.submit = WebForm_SaveScrollPositionSubmit;

theForm.oldOnSubmit = theForm.onsubmit;
theForm.onsubmit = WebForm_SaveScrollPositionOnSubmit;
WebForm_AutoFocus('txtHTNo');
document.getElementById('RegularExpressionValidator1').dispose = function() {
    Array.remove(Page_Validators, document.getElementById('RegularExpressionValidator1'));
}

document.getElementById('vreValidator').dispose = function() {
    Array.remove(Page_Validators, document.getElementById('vreValidator'));
}

document.getElementById('vrfValidator').dispose = function() {
    Array.remove(Page_Validators, document.getElementById('vrfValidator'));
}
//]]>
</script>
<span style="display: none !important;"><input type="hidden" name="__LASTFOCUS" id="__LASTFOCUS" value=""></span><span style="display: none !important;"><input type="hidden" name="__EVENTTARGET" id="__EVENTTARGET" value=""></span><span style="display: none !important;"><input type="hidden" name="__EVENTARGUMENT" id="__EVENTARGUMENT" value=""></span><span style="display: none !important;"><input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="/wEPDwUKLTUyNTM2ODAzMA9kFgQCCA8PFgIeBFRleHQFOOCwruCwguCwl+Cws+CwteCwvuCwsOCwgiwg4LCP4LCq4LGN4LCw4LC/4LCy4LGNIDIyLCAyMDI1ZGQCDQ9kFgICBQ9kFgJmD2QWJgIJD2QWAgIHDw8WAh8AZWRkAgsPDxYCHwAFCjI1NjExMTY3MTNkZAINDw8WAh8ABQM0NjVkZAIPDw8WAh8ABR5DSEVFREVMTEEgTEFLU0hNSSBOQVZZQSBNQU5BU1dkZAIRDw8WAh8ABQZBICAgICBkZAITDw8WAh8ABQggRU5HTElTSGRkAhUPDxYCHwAFCSBTQU5TS1JJVGRkAhcPDxYCHwAFD01BVEhFTUFUSUNTICBJQWRkAhkPDxYCHwAFD01BVEhFTUFUSUNTICBJQmRkAhsPDxYCHwAFB1BIWVNJQ1NkZAIdDw8WAh8ABQlDSEVNSVNUUllkZAIfDw8WAh8ABRMgRU5HTElTSCBQUkFDVElDQUxTZGQCIQ8PFgIfAAUFIDc2IFBkZAIjDw8WAh8ABQUgOTkgUGRkAiUPDxYCHwAFBSA3NSBQZGQCJw8PFgIfAAUFIDc1IFBkZAIpDw8WAh8ABQUgNjAgUGRkAisPDxYCHwAFBSA2MCBQZGQCLQ8PFgIfAAUFIDIwIFBkZGSVB4zug1qEMqraLYAYEAY0SkrV3Q=="></span><span style="display: none !important;"><input type="hidden" name="__VIEWSTATEGENERATOR" id="__VIEWSTATEGENERATOR" value="5338D94C"></span><span style="display: none !important;"><input type="hidden" name="__SCROLLPOSITIONX" id="__SCROLLPOSITIONX" value="0"></span><span style="display: none !important;"><input type="hidden" name="__SCROLLPOSITIONY" id="__SCROLLPOSITIONY" value="0"></span><span style="display: none !important;"><input type="hidden" name="__EVENTVALIDATION" id="__EVENTVALIDATION" value="/wEdAAOcuIwXQbJ+TXXO2/b9br1R25mTIbcP91/GqB57z2Eq3BsRKej6wdX4jURfxOzOxSBewUOl2CrwjbADMlH4rjm4tQ6T9g=="></span></form>
        <!-- 3 column Section End -->
                    
        <!-- 728x90 ad start -->
        <!-- include file = ads/d_bottom_728x90.htm -->
        <!-- 728x90 ad End -->
         <!--sticky footer menu-->
           <!--sticky footer menu-->
<div class="hm-scl-tumbs">
    <ul>
        <li>
            <a href="https://www.eenadu.net/videos" aria-label="Eenadu Videos">
                <div class="icon-hm1"></div>
                <p>Videos</p>
            </a>
        </li>
        <li>
            <a href="https://stories.eenadu.net/" aria-label="Eenadu Web Stories">
                <div class="icon-hm2"></div>
                <p>Web Stories</p>
            </a>
        </li>
        <li class="active">
            <a href="https://www.eenadu.net/" aria-label="Eenadu Home">
                <div class="icon-hm3"></div>
                <!-- <p>Home</p> -->
            </a>
        </li>
        <li>
            <a href="https://www.eenadu.net/trending-news" aria-label="Eenadu Most Read News">
                <div class="icon-hm4"></div>
                <p>Most Read</p>
            </a>
        </li>
        <li>
            <a href="https://www.eenadu.net/photos" aria-label="Eenadu Photos">
                <div class="icon-hm5"></div>
                <p>Photos</p>
            </a>
        </li>
    </ul>
</div>
<!--sticky footer menu-->
<!-- Footer Start -->
<div class="footer">
    <p style="margin-bottom: 10px; text-align: center;">
        © 2025  Ushodaya Enterprises Pvt. Ltd., All Rights Reserved. For digital advertisements Contact: 040 23318181<!--, eMail: digitalads@eenadu.in-->
    </p>
    <p>
        <span>Disclaimer</span> : eenadu.net is not responsible for any inadvertent error
        that may have crept in the results being published on NET. The results published
        on net are for the immediate information to the examinees. This does not constitute
        to be a legal document. While all efforts have been made to make the informat ion
        available on this website as authentic as possible,eenadu or any staff persons will
        not be responsible for any loss to persons caused by any shortcoming, defect or
        inaccuracy in the information available on website.
    </p>
</div>
<!-- Footer End -->
        <!-- Footer End -->
        <!-- include file = share/dialog-share-firstG.htm -->
    </div>
          
    
    <script src="../js/header.js"></script>


<div id="kins-kins-popup" style="color-scheme: initial; forced-color-adjust: initial; mask: initial; math-depth: initial; position: initial; position-anchor: initial; text-size-adjust: initial; appearance: initial; color: initial; direction: ltr; font-family: Rubik, sans-serif; font-feature-settings: initial; font-kerning: initial; font-optical-sizing: initial; font-palette: initial; font-size: medium; font-size-adjust: initial; font-stretch: initial; font-style: initial; font-synthesis: initial; font-variant: initial; font-variation-settings: initial; font-weight: initial; position-area: initial; text-orientation: initial; text-rendering: initial; text-spacing-trim: initial; -webkit-font-smoothing: initial; -webkit-locale: initial; -webkit-text-orientation: initial; -webkit-writing-mode: initial; writing-mode: initial; zoom: initial; accent-color: initial; place-content: initial; place-items: initial; place-self: initial; alignment-baseline: initial; anchor-name: initial; anchor-scope: initial; animation-composition: initial; animation: initial; app-region: initial; aspect-ratio: initial; backdrop-filter: initial; backface-visibility: initial; background: none; background-blend-mode: initial; baseline-shift: initial; baseline-source: initial; block-size: initial; border-block: initial; border: none; border-radius: initial; border-collapse: initial; border-end-end-radius: initial; border-end-start-radius: initial; border-inline: initial; border-start-end-radius: initial; border-start-start-radius: initial; inset: initial; box-decoration-break: initial; box-shadow: initial; box-sizing: border-box; break-after: initial; break-before: initial; break-inside: initial; buffered-rendering: initial; caption-side: initial; caret-color: initial; clear: initial; clip: initial; clip-path: initial; clip-rule: initial; color-interpolation: initial; color-interpolation-filters: initial; color-rendering: initial; columns: initial; column-fill: initial; gap: initial; column-rule: initial; column-span: initial; contain: initial; contain-intrinsic-block-size: initial; contain-intrinsic-size: initial; contain-intrinsic-inline-size: initial; container: initial; content: initial; content-visibility: initial; counter-increment: initial; counter-reset: initial; counter-set: initial; cursor: initial; cx: initial; cy: initial; d: initial; display: block; dominant-baseline: initial; empty-cells: initial; field-sizing: initial; fill: initial; fill-opacity: initial; fill-rule: initial; filter: initial; flex: initial; flex-flow: initial; float: initial; flood-color: initial; flood-opacity: initial; grid: initial; grid-area: initial; height: auto; hyphenate-character: initial; hyphenate-limit-chars: initial; hyphens: initial; image-orientation: initial; image-rendering: initial; initial-letter: initial; inline-size: initial; inset-block: initial; inset-inline: initial; interpolate-size: initial; isolation: initial; letter-spacing: initial; lighting-color: initial; line-break: initial; line-height: normal; list-style: initial; margin-block: initial; margin: 0px; margin-inline: initial; marker: initial; mask-type: initial; math-shift: initial; math-style: initial; max-block-size: initial; max-height: initial; max-inline-size: initial; max-width: initial; min-block-size: initial; min-height: initial; min-inline-size: initial; min-width: initial; mix-blend-mode: initial; object-fit: initial; object-position: initial; object-view-box: initial; offset: initial; opacity: initial; order: initial; orphans: initial; outline: initial; outline-offset: initial; overflow-anchor: initial; overflow-block: initial; overflow-clip-margin: initial; overflow-inline: initial; overflow-wrap: initial; overflow: initial; overlay: initial; overscroll-behavior-block: none; overscroll-behavior-inline: none; overscroll-behavior: none; padding-block: initial; padding: 0px; padding-inline: initial; page: initial; page-orientation: initial; paint-order: initial; perspective: initial; perspective-origin: initial; pointer-events: initial; position-try: initial; position-visibility: initial; quotes: initial; r: initial; resize: initial; rotate: initial; ruby-align: initial; ruby-position: initial; rx: initial; ry: initial; scale: initial; scroll-behavior: initial; scroll-initial-target: initial; scroll-margin-block: initial; scroll-margin: initial; scroll-margin-inline: initial; scroll-marker-group: initial; scroll-padding-block: initial; scroll-padding: initial; scroll-padding-inline: initial; scroll-snap-align: initial; scroll-snap-stop: initial; scroll-snap-type: initial; scroll-timeline: initial; scrollbar-color: initial; scrollbar-gutter: initial; scrollbar-width: initial; shape-image-threshold: initial; shape-margin: initial; shape-outside: initial; shape-rendering: initial; size: initial; speak: initial; stop-color: initial; stop-opacity: initial; stroke: initial; stroke-dasharray: initial; stroke-dashoffset: initial; stroke-linecap: initial; stroke-linejoin: initial; stroke-miterlimit: initial; stroke-opacity: initial; stroke-width: initial; tab-size: initial; table-layout: initial; text-align: left; text-align-last: initial; text-anchor: initial; text-box: initial; text-combine-upright: initial; text-decoration: none; text-decoration-skip-ink: initial; text-emphasis: initial; text-emphasis-position: initial; text-indent: initial; text-overflow: initial; text-shadow: initial; text-transform: initial; text-underline-offset: initial; text-underline-position: initial; text-wrap: wrap; timeline-scope: initial; touch-action: initial; transform: initial; transform-box: initial; transform-origin: initial; transform-style: initial; transition: initial; translate: initial; user-select: initial; vector-effect: initial; vertical-align: initial; view-timeline: initial; view-transition-class: initial; view-transition-name: initial; visibility: initial; border-spacing: initial; -webkit-box-align: initial; -webkit-box-decoration-break: initial; -webkit-box-direction: initial; -webkit-box-flex: initial; -webkit-box-ordinal-group: initial; -webkit-box-orient: initial; -webkit-box-pack: initial; -webkit-box-reflect: initial; -webkit-line-break: initial; -webkit-line-clamp: initial; -webkit-mask-box-image: initial; -webkit-print-color-adjust: initial; -webkit-rtl-ordering: initial; -webkit-ruby-position: initial; -webkit-tap-highlight-color: initial; -webkit-text-combine: initial; -webkit-text-decorations-in-effect: initial; -webkit-text-fill-color: initial; -webkit-text-security: initial; -webkit-text-stroke: initial; -webkit-user-drag: initial; white-space-collapse: collapse; widows: initial; width: auto; will-change: initial; word-break: initial; word-spacing: initial; x: initial; y: initial; z-index: initial;"><style>
                    #kins_root {
                        display: block !important;
                    }
                </style><div id="kins_root" style="color-scheme: initial; forced-color-adjust: initial; mask: initial; math-depth: initial; position: initial; position-anchor: initial; text-size-adjust: initial; appearance: initial; color: initial; direction: ltr; font-family: Rubik, sans-serif; font-feature-settings: initial; font-kerning: initial; font-optical-sizing: initial; font-palette: initial; font-size: medium; font-size-adjust: initial; font-stretch: initial; font-style: initial; font-synthesis: initial; font-variant: initial; font-variation-settings: initial; font-weight: initial; position-area: initial; text-orientation: initial; text-rendering: initial; text-spacing-trim: initial; -webkit-font-smoothing: initial; -webkit-locale: initial; -webkit-text-orientation: initial; -webkit-writing-mode: initial; writing-mode: initial; zoom: initial; accent-color: initial; place-content: initial; place-items: initial; place-self: initial; alignment-baseline: initial; anchor-name: initial; anchor-scope: initial; animation-composition: initial; animation: initial; app-region: initial; aspect-ratio: initial; backdrop-filter: initial; backface-visibility: initial; background: none; background-blend-mode: initial; baseline-shift: initial; baseline-source: initial; block-size: initial; border-block: initial; border: none; border-radius: initial; border-collapse: initial; border-end-end-radius: initial; border-end-start-radius: initial; border-inline: initial; border-start-end-radius: initial; border-start-start-radius: initial; inset: initial; box-decoration-break: initial; box-shadow: initial; box-sizing: border-box; break-after: initial; break-before: initial; break-inside: initial; buffered-rendering: initial; caption-side: initial; caret-color: initial; clear: initial; clip: initial; clip-path: initial; clip-rule: initial; color-interpolation: initial; color-interpolation-filters: initial; color-rendering: initial; columns: initial; column-fill: initial; gap: initial; column-rule: initial; column-span: initial; contain: initial; contain-intrinsic-block-size: initial; contain-intrinsic-size: initial; contain-intrinsic-inline-size: initial; container: initial; content: initial; content-visibility: initial; counter-increment: initial; counter-reset: initial; counter-set: initial; cursor: initial; cx: initial; cy: initial; d: initial; display: block; dominant-baseline: initial; empty-cells: initial; field-sizing: initial; fill: initial; fill-opacity: initial; fill-rule: initial; filter: initial; flex: initial; flex-flow: initial; float: initial; flood-color: initial; flood-opacity: initial; grid: initial; grid-area: initial; height: auto; hyphenate-character: initial; hyphenate-limit-chars: initial; hyphens: initial; image-orientation: initial; image-rendering: initial; initial-letter: initial; inline-size: initial; inset-block: initial; inset-inline: initial; interpolate-size: initial; isolation: initial; letter-spacing: initial; lighting-color: initial; line-break: initial; line-height: normal; list-style: initial; margin-block: initial; margin: 0px; margin-inline: initial; marker: initial; mask-type: initial; math-shift: initial; math-style: initial; max-block-size: initial; max-height: initial; max-inline-size: initial; max-width: initial; min-block-size: initial; min-height: initial; min-inline-size: initial; min-width: initial; mix-blend-mode: initial; object-fit: initial; object-position: initial; object-view-box: initial; offset: initial; opacity: initial; order: initial; orphans: initial; outline: initial; outline-offset: initial; overflow-anchor: initial; overflow-block: initial; overflow-clip-margin: initial; overflow-inline: initial; overflow-wrap: initial; overflow: initial; overlay: initial; overscroll-behavior-block: none; overscroll-behavior-inline: none; overscroll-behavior: none; padding-block: initial; padding: 0px; padding-inline: initial; page: initial; page-orientation: initial; paint-order: initial; perspective: initial; perspective-origin: initial; pointer-events: initial; position-try: initial; position-visibility: initial; quotes: initial; r: initial; resize: initial; rotate: initial; ruby-align: initial; ruby-position: initial; rx: initial; ry: initial; scale: initial; scroll-behavior: initial; scroll-initial-target: initial; scroll-margin-block: initial; scroll-margin: initial; scroll-margin-inline: initial; scroll-marker-group: initial; scroll-padding-block: initial; scroll-padding: initial; scroll-padding-inline: initial; scroll-snap-align: initial; scroll-snap-stop: initial; scroll-snap-type: initial; scroll-timeline: initial; scrollbar-color: initial; scrollbar-gutter: initial; scrollbar-width: initial; shape-image-threshold: initial; shape-margin: initial; shape-outside: initial; shape-rendering: initial; size: initial; speak: initial; stop-color: initial; stop-opacity: initial; stroke: initial; stroke-dasharray: initial; stroke-dashoffset: initial; stroke-linecap: initial; stroke-linejoin: initial; stroke-miterlimit: initial; stroke-opacity: initial; stroke-width: initial; tab-size: initial; table-layout: initial; text-align: left; text-align-last: initial; text-anchor: initial; text-box: initial; text-combine-upright: initial; text-decoration: none; text-decoration-skip-ink: initial; text-emphasis: initial; text-emphasis-position: initial; text-indent: initial; text-overflow: initial; text-shadow: initial; text-transform: initial; text-underline-offset: initial; text-underline-position: initial; text-wrap: wrap; timeline-scope: initial; touch-action: initial; transform: initial; transform-box: initial; transform-origin: initial; transform-style: initial; transition: initial; translate: initial; user-select: initial; vector-effect: initial; vertical-align: initial; view-timeline: initial; view-transition-class: initial; view-transition-name: initial; visibility: initial; border-spacing: initial; -webkit-box-align: initial; -webkit-box-decoration-break: initial; -webkit-box-direction: initial; -webkit-box-flex: initial; -webkit-box-ordinal-group: initial; -webkit-box-orient: initial; -webkit-box-pack: initial; -webkit-box-reflect: initial; -webkit-line-break: initial; -webkit-line-clamp: initial; -webkit-mask-box-image: initial; -webkit-print-color-adjust: initial; -webkit-rtl-ordering: initial; -webkit-ruby-position: initial; -webkit-tap-highlight-color: initial; -webkit-text-combine: initial; -webkit-text-decorations-in-effect: initial; -webkit-text-fill-color: initial; -webkit-text-security: initial; -webkit-text-stroke: initial; -webkit-user-drag: initial; white-space-collapse: collapse; widows: initial; width: auto; will-change: initial; word-break: initial; word-spacing: initial; x: initial; y: initial; z-index: initial;"></div></div></body></html>


check this out and see how are they fecting data and i now want to fetech using scrapper. please give me code
