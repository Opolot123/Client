# Client
import requests

BASE_URL = 'http://127.0.0.1:5000/items'

def get_items():
    response = requests.get(BASE_URL)
    print(response.json())

def get_item(item_id):
    response = requests.get(f'{BASE_URL}/{item_id}')
    print(response.json())

def create_item(name):
    response = requests.post(BASE_URL, json={"name": name})
    print(response.json())

def update_item(item_id, name):
    response = requests.put(f'{BASE_URL}/{item_id}', json={"name": name})
    print(response.json())

def delete_item(item_id):
    response = requests.delete(f'{BASE_URL}/{item_id}')
    print('Deleted' if response.status_code == 204 else 'Error')

if __name__ == '__main__':
    # Example usage
    get_items()
    create_item('New Item')
    get_items()
    update_item(1, 'Updated Item 1')
    get_items()
    delete_item(2)
    get_items()

