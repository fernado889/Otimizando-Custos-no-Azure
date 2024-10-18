# Otimizando-Custos-no-Azure
from azure.identity import DefaultAzureCredential
from azure.mgmt.resource import SubscriptionClient
from azure.mgmt.compute import ComputeManagementClient
from azure.mgmt.resource import ResourceManagementClient

# Autenticar-se no Azure
credential = DefaultAzureCredential()
subscription_client = SubscriptionClient(credential)

# Substitua pelo seu ID de assinatura
subscription_id = 'YOUR_SUBSCRIPTION_ID'

# Criar clientes
compute_client = ComputeManagementClient(credential, subscription_id)
resource_client = ResourceManagementClient(credential, subscription_id)

# Listar todas as VMs e seus status
def list_virtual_machines():
    print("Listando VMs:")
    for vm in compute_client.virtual_machines.list_all():
        print(f"Nome: {vm.name}, Estado: {vm.power_state}, Localização: {vm.location}")

# Verificar uso e recomendar desligar VMs inativas
def optimize_costs():
    print("Analisando VMs para otimização de custos:")
    for vm in compute_client.virtual_machines.list_all():
        # Exemplo simplificado: verificar se a VM está parada
        if vm.power_state == "VM de parada":
            print(f"Recomendação: Considere desligar a VM '{vm.name}' para economizar custos.")

# Executar as funções
list_virtual_machines()
optimize_costs()
