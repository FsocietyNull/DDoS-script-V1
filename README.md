import requests
import concurrent.futures
import time

def send_request(url):
    try:
        response = requests.get(url, timeout=1)
        print(f"Request sent. Status code: {response.status_code}")
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")

def main():
    url = input("Enter the website URL: ")
    num_requests = int(input("Enter the number of requests to send: "))
    num_threads = int(input("Enter the number of threads to use: "))

    start_time = time.time()

    with concurrent.futures.ThreadPoolExecutor(max_workers=num_threads) as executor:
        futures = [executor.submit(send_request, url) for _ in range(num_requests)]

        for future in concurrent.futures.as_completed(futures):
            future.result()

    end_time = time.time()

    print(f"Requests sent in {end_time - start_time} seconds")

if __name__ == "__main__":
    main()
