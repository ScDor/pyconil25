
# Pydantic Settings

load settings from environment variables with types

<v-clicks>

````md magic-move

```python{|4|5|6|10}
import os, json

APP_NAME = os.getenv("APP_NAME", "UNKNOWN APP")
DEBUG = os.getenv("DEBUG", "").lower() in ("1","true","yes","y")
PORT = int(os.getenv("PORT", "8000"))
ALLOWED_HOSTS = json.loads(os.getenv("ALLOWED_HOSTS", "[]"))
API_KEY = os.getenv("API_KEY", "")

print(APP_NAME, f"port={PORT}", f"debug={DEBUG}", f"hosts={ALLOWED_HOSTS}",
      '**********' if API_KEY else '')
```
```python{4|5|7|10}
from pydantic_settings import BaseSettings, SettingsConfigDict
from pydantic import SecretStr

class Settings(BaseSettings):
    model_config = SettingsConfigDict(env_file=".env")  # loads .env too
    app_name: str = "UNKNOWN APP"
    debug: bool = False
    port: int = 8000
    allowed_hosts: list[str] = []
    api_key: SecretStr

s = Settings()
print(s.app_name, f"port={s.port}", f"debug={s.debug}", f"hosts={s.allowed_hosts}", 
      f"api_key={s.api_key}")
```
````
</v-clicks>


---

# Pydantic Settings: pyproject.toml

use builtin pyproject parsing; env/.env overrides

<v-clicks>

````md magic-move

```python{|5|6}
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

