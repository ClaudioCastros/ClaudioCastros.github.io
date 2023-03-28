# Manipular sessões de um arquivo .ini

## Excluir sessão de configuração.
with open("test.ini", "r") as f:
    p.readfp(f)

print(p.sections())
p.remove_section('a')
print(p.sections())

with open("test.ini", "w") as f:
    p.write(f)

# this just verifies that [b] section is still there
with open("test.ini", "r") as f:
    print(f.read())
    
    
# Create new section
config.read('~/test/config.conf')
config = configparser.ConfigParser()
config.read('config.conf')
config.add_section('Section2')
config.set('Section2', 'name', 'Mary')
config.set('Section2', 'number', '6')
with open('config.conf', 'w') as configfile:
    config.write(configfile)
    
# Update sessão
from ConfigParser import SafeConfigParser
parser = SafeConfigParser()
parser.read('properties.ini')
dhana = {'key': 'valu11'}
parser.set('CAMPAIGNS', 'zoho_next_campaign_map', str(dhana))
with open("properties.ini", "w+") as configfile:
    parser.write(configfile)
