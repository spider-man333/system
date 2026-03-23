# Web用户管理（Django）

## 项目简介
本项目是一个基于 Django 的后台管理系统示例，包含：

- 登录（验证码校验）
- 注册（写入数据库 Admin 表）
- 部门管理
- 用户管理
- 靓号管理
- 管理员管理
- 任务管理（含 Ajax 示例）
- 订单管理
- 数据统计（ECharts/Highcharts）
- 文件上传
- 城市管理

## 技术栈
- Python
- Django
- MySQL（`mysqlclient`）
- Bootstrap 3

## 目录结构
- `manage.py`：Django 管理入口
- `configuration/`：项目配置（settings/urls/wsgi/asgi）
- `app01/`：业务应用
  - `views/`：视图函数（包含登录/注册）
  - `templates/`：模板文件（`login.html`、`register.html` 等）
  - `static/`：静态资源（Bootstrap、JS、图表库等）
  - `middleware/`：中间件（登录鉴权）
  - `models.py`：数据模型（`Admin`、`Department` 等）
  - `migrations/`：迁移文件

## 环境要求
- Python 3.x
- MySQL 5.7/8.x

## 安装依赖
建议使用虚拟环境：

```bash
pip install -r requirements.txt
```

## 数据库配置
数据库配置位于：`configuration/settings.py`。

默认使用 MySQL：

- DB：`lk_day`
- Host：`127.0.0.1`
- Port：`3306`

请根据你本机 MySQL 账号密码修改：

- `USER`
- `PASSWORD`

## 初始化数据库（首次运行）
在项目根目录（包含 `manage.py`）执行：

```bash
python manage.py makemigrations
python manage.py migrate
```

## 启动项目
在项目根目录执行：

```bash
python manage.py runserver 0.0.0.0:8000
```

启动后访问：

- 登录：`http://127.0.0.1:8000/login/`
- 注册：`http://127.0.0.1:8000/register/`

## 登录与注册说明
- 登录逻辑：`app01/views/account.py` -> `login`
  - 使用图片验证码接口：`/image/code/`
  - 登录成功后写入 session：`request.session["info"]`

- 注册逻辑：`app01/views/account.py` -> `register`
  - 注册信息写入 `Admin` 表（`app01/models.py` -> `Admin`）
  - 密码使用项目内 `md5` 工具加密后保存

## 主要路由
路由配置文件：`configuration/urls.py`。

常用入口：

- `/login/` 登录
- `/register/` 注册
- `/logout/` 注销
- `/admin/list/` 管理员列表
- `/depart/list/` 部门列表
- `/user/list/` 用户列表
- `/pretty/list/` 靓号列表
- `/task/list/` 任务列表
- `/order/list/` 订单列表
- `/chart/list/` 数据统计
- `/upload/list/` 上传
- `/city/list/` 城市

## 常见问题
- **启动报错：`ModuleNotFoundError: No module named 'day16'`**
  - 本项目使用 `configuration` 作为 settings/urlconf 包，确保：
    - `manage.py` 中 `DJANGO_SETTINGS_MODULE` 为 `configuration.settings`
    - `configuration/settings.py` 中 `ROOT_URLCONF = 'configuration.urls'`

- **数据库连接失败**
  - 检查 MySQL 是否启动
  - 检查 `configuration/settings.py` 中的账号密码、库名、端口

## License
本项目为学习/演示用途。
