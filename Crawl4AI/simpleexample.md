```py
import asyncio
from crawl4ai import AsyncWebCrawler, BrowserConfig, CrawlerRunConfig

async def main():
    # 1) Reference your persistent data directory
    browser_config = BrowserConfig(
        headless=True,             # 'True' for automated runs
        verbose=True,
        use_managed_browser=True,  # Enables persistent browser strategy
        browser_type="chromium",
        user_data_dir="/path/to/my-chrome-profile"
    )

    # 2) Standard crawl config
    crawl_config = CrawlerRunConfig(
        wait_for="css:.logged-in-content"
    )

    async with AsyncWebCrawler(config=browser_config) as crawler:
        result = await crawler.arun(url="https://example.com/private", config=crawl_config)
        if result.success:
            print("Successfully accessed private data with your identity!")
        else:
            print("Error:", result.error_message)

if __name__ == "__main__":
    asyncio.run(main())

```