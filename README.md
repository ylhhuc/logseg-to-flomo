import os
import re
import requests

def send_to_flomo(content):
    url = '你的flomo api/'
    headers = {'Content-Type': 'application/json'}
    payload = {'content': content}
    response = requests.post(url, json=payload)
    return response.text

def process_markdown_file(file_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        content = file.read()
    
    # 替换 [[...]] 为 #...
    modified_content = re.sub(r'\[\[([^\]]+)\]\]', r'#\1', content)
    return modified_content

def process_directory(directory):
    # 遍历目录中的所有Markdown文件
    for filename in os.listdir(directory):
        if filename.endswith(".md"):
            file_path = os.path.join(directory, filename)
            modified_content = process_markdown_file(file_path)
            result = send_to_flomo(modified_content)
            print(f"Processed {filename}: {result}")

# 提供你的Markdown文件所在的文件夹路径
process_directory(r'E:\logseq\journals\journals')



如果你需要把logseg到处的文件放到一个文件夹下面，再将地址替换即可
