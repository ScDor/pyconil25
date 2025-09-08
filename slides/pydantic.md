
# Type Hints That Actually Do Something 

<v-clicks>

````md magic-move

```python{1|2-3|4-5|6-7|8|10|}
def create_user(name: Any, age: Any, email: Any) -> dict:
    if not isinstance(name, str):
        raise ValueError("name must be string")
    if not isinstance(age, int):
        raise ValueError("age must be int")
    if "@" not in email:
        raise ValueError("invalid email")
    return {"name": name, "age": age, "email": email}

user = create_user("Alice", 25, "alice@example.com")
```
```python{3-6|8-9}
from pydantic import BaseModel, EmailStr

class User(BaseModel):
    name: str
    age: int
    email: EmailStr

user = User(name="Alice", age="25", email="alice@example.com")
print(user.age, type(user.age))  # 25 <class 'int'>
```
````

</v-clicks>

---

# Env Vars: Now With 100% Less String Parsing Hell

<v-clicks>

````md magic-move

```python{|4|5|6|10}
import os, json

DEBUG = os.getenv("DEBUG", "").lower() in ("1","true","yes","y")
PORT = int(os.getenv("PORT", "8000"))
ALLOWED_HOSTS = json.loads(os.getenv("ALLOWED_HOSTS", "[]"))
API_KEY = os.getenv("API_KEY", "")

print(f"port={PORT}", f"debug={DEBUG}", 
      f"hosts={ALLOWED_HOSTS}", 
      "api_key=" + "**********" if API_KEY else "")
```
```python{4-9|7|9|11}
from pydantic_settings import BaseSettings, SettingsConfigDict
from pydantic import SecretStr

class Settings(BaseSettings):
    debug: bool = False
    port: int = 8000
    allowed_hosts: list[str] = []
    api_key: SecretStr
    model_config = SettingsConfigDict(env_file=".env")  # optional!

s = Settings()
print(s.app_name, f"port={s.port}", f"debug={s.debug}", f"hosts={s.allowed_hosts}", 
      f"api_key={s.api_key}")
```
````
</v-clicks>


