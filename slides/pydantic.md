
# Pydantic Settings

Goal: load settings from environment variables with types

```
Inputs:
APP_NAME=Demo DEBUG=1 PORT=8000 ALLOWED_HOSTS='["a.com","b.com"]' API_KEY=secret
```

<v-clicks>

````md magic-move

```python
import os, json

APP_NAME = os.getenv("APP_NAME", "UNKNOWN APP")
DEBUG = os.getenv("DEBUG", "false").lower() in ("1","true","yes","y")
PORT = int(os.getenv("PORT", "8000"))
ALLOWED_HOSTS = json.loads(os.getenv("ALLOWED_HOSTS", "[]"))
API_KEY = os.getenv("API_KEY", "")

print(APP_NAME, f"port={PORT}", f"debug={DEBUG}", f"hosts={ALLOWED_HOSTS}",
      '**********' if API_KEY else '')
```
```python
from pydantic_settings import BaseSettings, SettingsConfigDict
from pydantic import SecretStr

class Settings(BaseSettings):
    model_config = SettingsConfigDict(env_file=".env")  # loads .env too
    app_name: str = "UNKNOWN APP"
    debug: bool = False
    port: int = 8000
    allowed_hosts: list[str] = []
    api_key: SecretStr = SecretStr("")

s = Settings()
print(s.app_name, f"port={s.port}", f"debug={s.debug}", f"hosts={s.allowed_hosts}", 
      f"api_key={s.api_key}")
```
````
</v-clicks>

```
Output:
Demo port=8000 debug=True hosts=['a.com', 'b.com'] api_key=**********
```

---

# Pydantic Settings: pyproject.toml

Goal: use builtin pyproject parsing; env/.env overrides

<v-clicks>

````md magic-move

```python
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(
        pyproject_toml_table="tool.myapp",
        env_file=".env",
    )
    app_name: str
    debug: bool = False
    port: int = 8000

s = Settings()
print(s.app_name, s.port, s.debug)
```
````

</v-clicks>

```
Output:
My app 9000 True
```
