import requests

def send_requests(url, num_requests):
    for i in range(num_requests):
        try:
            response = requests.get(url)
            print(f"Request {i+1} sent. Status code: {response.status_code}")
        except requests.exceptions.RequestException as e:
            print(f"Request {i+1} failed: {e}")

def main():
    url = input("Enter the website URL: ")
    num_requests = int(input("Enter the number of requests to send: "))
    send_requests(url, num_requests)

if __name__ == "__main__":
    main()
