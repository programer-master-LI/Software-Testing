# pytest测试工具
测试文件以test_开头，测试函数也以test_开头
自动化测试代码，确保程序功能正确、修改后不引入新错误。
Pytest 是 Python 自动化测试框架，用于 验证代码功能是否正确，支持单元测试、集成测试、接口测试和自动化测试
Pytest 的优点
1.语法简单
Python 自带的 unittest：
import unittest
class TestAdd(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)

Pytest：
def test_add():
    assert add(2, 3) == 5
更简洁。
2.自动发现测试文件
例如：
project/
├── app.py
├── test_app.py
├── test_api.py
直接运行：
pytest
自动找到所有测试。（因为测试文件以test_开头）
3.生成测试报告
pytest --html=report.html
可生成测试报告，方便课程作业和项目展示。
4.支持参数化测试
同一个测试 跑多组数据：
import pytest
@pytest.mark.parametrize(
    "a,b,result",
    [
        (1,2,3),
        (2,3,5),
        (3,4,7)
    ]
)
def test_add(a,b,result):
    assert add(a,b)==result

测试类型	Pytest用途
单元测试	测试网页解析函数
集成测试	测试爬取→解析→保存流程
系统测试	测试整个爬虫运行
性能测试	配合 pytest-benchmark
接口测试	测试 API 服务

1. 单元测试（Unit Testing）
测试单个函数或模块是否正常工作。
例如：
def add(a, b):
    return a + b
def test_add():
    assert add(2, 3) == 5      （验证开发的代码是否正确）
运行：
pytest
结果：
1 passed

2. 回归测试（Regression Testing）
当你修改代码后，可以快速检查 原有功能是否被破坏。
例如：
原来：
def add(a, b):
    return a + b
后来误改成：
def add(a, b):
    return a - b
Pytest 会立即发现错误：
FAILED test_add
assert -1 == 5

3. 自动化测试
对于大型项目（如 YOLO、爬虫、Web 系统），手动测试很耗时。
Pytest 可以一次运行所有测试：
pytest
自动检查几十甚至几百个功能。

4. 集成测试（Integration Testing）
测试多个模块协同工作是否正常。
例如：
def login():
    ...
def get_user_info():
    ...
测试登录后是否能正确获取用户信息。

5. 接口测试（API Testing）
测试 Web API。
例如：
import requests
def test_api():
    r = requests.get("http://127.0.0.1:5000/users")
    assert r.status_code == 200          （assert断言）
适用于：
Flask
Django
FastAPI
Spring Boot（通过 HTTP 调用）

# 进阶内容
高级特性是编写大型、可维护、高效测试套件
1. Fixture（夹具）
Fixture 用于准备测试数据、初始化环境、连接数据库等。
import pytest

@pytest.fixture
def user():
    return {
        "name": "Tom",
        "age": 20
    }

def test_user(user):
    assert user["name"] == "Tom"

4. 测试类
class TestCalculator:

    def test_add(self):
        assert 1+2 == 3

    def test_sub(self):
        assert 5-2 == 3

运行：

pytest

自动发现类中的测试。

10. 并发测试
安装：
pip install pytest-xdist
运行：
pytest -n 4
表示：
4个CPU核心同时执行测试
原来：
100个测试
10分钟
变成：
2~3分钟

11. API测试
以 FastAPI 为例：
from fastapi.testclient import TestClient
client = TestClient(app)
def test_home():
    response = client.get("/")
    assert response.status_code == 200

11. API测试
以 FastAPI 为例：
from fastapi.testclient import TestClient
client = TestClient(app)
def test_home():
    response = client.get("/")
    assert response.status_code == 200






    
