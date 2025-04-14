Problem identified and solution(Ordered by the time the problem is discoverd):
1. main.py didn't handle cases when no method is provided. We can fix it easily by setting it to "GET"
2. The provided programming file is named main.py, so the running code should be "python main.py {yaml file name}" instead of python monitor.py {yaml file}
3. The program didn't check if the response time is <500 ms which is required in the pdf description, which is fixed with the following code:
        response_time = response.elapsed.total_seconds() //using stack overflow can easily find out the method.
        if 200 <= response.status_code < 300 and response_time<0.5:
4. Domain name is read incorrectly, certain URL can have two continuous "//" based on google search. https://example.com//dashboard is consider a valid URL 
and domain = endpoint["url"].split("//")[-1].split("/")[0] will get the incorrect result. Here's the fix :
        domain = endpoint["url"].split("//")[1].split("/")[0]
5. Domain didn't ignore port number, we should take care of that. A sample test is added to sample.yaml and "localhost has 100% availability percentage" is returned, The fixed code is the following:
        domain = endpoint["url"].split("//")[1].split("/")[0].split(":")[0]

How to install the code: You can download the files as a folder from github and open the folder with VS code. Make sure you do pip install pyyaml and pip install requests to install all libraries.

How to run/stop: In the commander, type "python main.py sample.yaml" or any other yaml files. "ctrl+c" to stop the command.

Expected result: We are expected to see "xxx has y% availability percentage every 15 seconds." for every different domain.

The results are done independently with a little online search
