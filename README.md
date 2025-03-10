# WA_ID_Finder

Info on app - 

Selenium being used in Streamlit


This code works because it’s been carefully configured to run in headless environments and to ensure browser–driver compatibility. Here are the key points:

1. **Driver Version Management:**
   * The code uses **webdriver_manager** with an explicit driver version (e.g., `"120.0.6099.224"`). This makes sure that the ChromeDriver downloaded matches the version of Chromium installed on the system. If the driver and browser versions don’t match, you can get errors like “session not created.”
2. **Headless Operation and Stability:**
   * It sets Chrome options such as `--headless`, `--disable-gpu`, and `--no-sandbox`. These options allow the browser to run without a graphical interface and with reduced resource usage.
   * The additional flag `--disable-dev-shm-usage` is crucial in containerized or cloud environments where the shared memory size may be limited. This flag forces Chrome to avoid using `/dev/shm` (shared memory), which can otherwise lead to the browser tab crashing.
3. **Extracting API Details:**
   * The code navigates to a specific URL and leverages Chrome’s performance logging to capture network requests. This logging allows the script to extract the GraphQL endpoint URL and the required API key directly from the HTTP headers of a POST request, which is essential for making subsequent API calls.
4. **Including Chromium in `package.txt`:**
   * In deployment environments like Streamlit Cloud or Docker containers, the operating system may not have a full version of Google Chrome installed by default. By specifying **Chromium** in your `package.txt` (or requirements file), you ensure that the necessary browser binary is installed and available.
   * This guarantees that Selenium can actually launch a browser instance. Without Chromium (or a similar browser) installed, Selenium would fail to find the executable it needs to control, leading to runtime errors.
5. **Using a Selenium Base (or Base Configuration):**
   * Using a base configuration for Selenium—sometimes referred to as “SeleniumBase” or simply a standardized initialization setup—ensures that your driver is configured consistently across different parts of your application.
   * It simplifies managing common settings (like headless mode and various Chrome flags) and can help avoid issues that might arise from misconfiguration. This makes your automation code more robust and easier to maintain, especially in complex or cloud-based deployments.

In summary, the code works because it carefully matches the driver to the browser version, configures Chrome to run reliably in a headless, resource-constrained environment, and extracts the necessary API details from network logs. Specifying Chromium in your package list and using a base Selenium configuration ensures that all these components are available and correctly set up when your app runs.
