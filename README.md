# DataLabeling
### README: Verification of Business details using Scraping 
            --If the details are exact match Label {yes/no).
            --Redirected Url created if any.
#### Overview
This Python code automates the verification of business details by cross-referencing entries from a dataset against live web content. The script efficiently handles large data volumes, utilizing web scraping and text matching techniques to validate the accuracy of business information such as names, addresses, and cities by comparing them with the corresponding website content.

#### Prerequisites

- **Python Version**: Python 3.x
- **Required Libraries**:
  - `requests`: Handles HTTP requests to fetch web content.
  - `BeautifulSoup` (from `bs4`): Facilitates HTML parsing and data extraction from webpage content.
  - `pandas`: Enables data manipulation and handling of Excel files.

To install the required libraries, execute the following command in your environment:
```bash
pip install requests beautifulsoup4 pandas
```

#### Workflow Description

1. **Data Ingestion**:
   - The script begins by ingesting data from an Excel file (`Label_Data_Lily.xlsx`) into a `pandas` DataFrame. It targets a specific subset of rows (182001 to 182500) within the dataset. This subset includes crucial fields such as `URL`, `Business_Name`, `Address`, and `City`.

2. **Web Content Retrieval**:
   - The `fetch_website_content(url)` function is implemented to perform HTTP GET requests for fetching web page content. 
   - The function checks for HTTP redirects and records the final destination URL if a redirect occurs.
   - The response content is parsed using `BeautifulSoup`, converting the raw HTML into a structured format that facilitates element search and text extraction.

3. **Business Information Validation**:
   - The `check_match(soup, business_name, address, city)` function is designed to perform a text-based validation of the business information. 
   - To ensure robust matching, all strings are normalized to lowercase to mitigate case-sensitivity issues during the search.
   - The function evaluates whether the business name and either the address or city appear within the parsed HTML content, marking a match if both criteria are satisfied.

4. **Batch Processing and Data Augmentation**:
   - The script iterates over each record in the selected data subset. For each entry:
     - It invokes the web content retrieval function.
     - The retrieved content is then validated against the corresponding business details.
     - The script appends the validation result and the final URL (post-redirection) to the DataFrame.
   - This iterative approach ensures that each business record is systematically verified against live website content.

5. **Output Generation**:
   - Upon completing the processing loop, the script saves the augmented DataFrame—including match results and any redirection URLs—to a new Excel file (`Labeled_Data.xlsx`). This output file serves as the final deliverable, providing a comprehensive record of the verification results.

#### Execution Instructions
1. **File Path Configuration**: Ensure that the Excel file (`Label_Data_Lily.xlsx`) is located in the same directory as the script, or update the file path in the code accordingly.
2. **Script Execution**: Run the script in your Python environment. The script processes the data and saves the results to `Labeled_Data.xlsx`.
3. **Output Review**: The output file will contain additional columns for match results (`match`) and the final URLs after redirection (`redirected_url`).

#### Technical Considerations

- **HTTP Handling**: The script incorporates basic exception handling for network-related errors, such as timeouts, using `requests.exceptions.RequestException`. This ensures that the script can skip problematic URLs without terminating execution.

#### Potential Enhancements

- **NLP Integration**: Implement natural language processing (NLP) techniques to improve the accuracy of business detail verification, particularly for unstructured web content.
  
- **Detailed Logging**: Enhance the script with more granular logging capabilities to track the processing of each record, including success/failure states and error handling outcomes.
