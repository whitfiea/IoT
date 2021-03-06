---

copyright:
  years: 2016, 2018
lastupdated: "2018-05-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Controllo dell'accesso al gateway
{: #gateway-access-control}

I dispositivi gateway sono una classe specializzata di dispositivi che possono agire per conto di altri dispositivi. I gruppi di risorse gateway definiscono in una organizzazione quali gateway possono interagire al posto di quali dispositivi. I ruoli gateway determinano la capacità del gateway di registrare i dispositivi in Watson IoT Platform.
{: #shortdesc}

Utilizzi i gruppi di risorse per consentire ai gateway di agire per conto di un sottoinsieme dei dispositivi di un'organizzazione. I gateway possono solo pubblicare o sottoscrivere messaggi per se stessi e per conto di dispositivi che si trovano nel loro gruppo di risorse. 

Quando viene creato un nuovo gateway, viene creato anche un gruppo di risorse predefinito che viene assegnato al gateway. Il gruppo di risorse predefinito non può essere rimosso dal gateway. I gateway esistenti senza gruppi di risorse possono continuare ad agire per conto di tutti i dispositivi dell'organizzazione.

Per informazioni sulla pubblicazione di eventi dai dispositivi gateway tramite API, consulta [API HTTP per i dispositivi gateway](gw_api.html).

## Assegnazione di un ruolo a un gateway
{: #gw_roles}

Per assegnare un gateway a un gruppo di risorse, devi prima assegnare il gateway a un ruolo. Ai gateway appena creati viene assegnato il ruolo *Privileged Gateway* per impostazione predefinita e vengono assegnati a un gruppo di risorse predefinito. I gateway con il ruolo privilegiato possono registrare automaticamente i dispositivi, che vengono aggiunti al gruppo di risorse predefinito.

I gateway con il ruolo *Standard Gateway* non possono registrare automaticamente i dispositivi. 

Una volta assegnato a un gateway un gruppo di risorse, il gateway può agire solo per conto dei dispositivi di quel gruppo di risorse e di se stesso, anche se il suo ruolo viene modificato.

Per ulteriori informazioni sui ruoli del gateway, consulta [Ruoli gateway](../roles_index.html#gateway_roles).

Per assegnare un ruolo a un gateway, utilizza la seguente API dove *${clientID}* è il ClientID codificato URL nel formato *d:${orgId}:${typeId}:${deviceId}* per i dispositivi o *g:${orgId}:${typeId}:${deviceId}* per i gateway:

```
PUT /authorization/devices/${clientID}/roles

Request Body:
{
    "roles": [
        {
            "roleId": "PD_STANDARD_GW_DEVICE",
            "roleStatus": 1
        }
    ]
}

Request Response: 200
{
    "roles": [
        {
            "roleId": "PD_STANDARD_GW_DEVICE",
            "roleStatus": 1
        }
    ],
    "rolesToGroups": {
        "PD_STANDARD_GW_DEVICE": ["gw_def_res_grp:abcdef:gatewayTypeId:gatewayDeviceId"]
    }
}
```

Per i dettagli dello schema richiesto, consulta [{{site.data.keyword.iot_full}} Limited Gateway API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles){: new_window}.

## Aggiunta dei dispositivi e loro rimozione da un gruppo di risorse.
{: #devices_groups}

Prima che un gateway con il ruolo *Gateway standard* possa agire al posto di un dispositivo, esso deve essere un membro del gruppo di risorse assegnato al gateway. Per aggiungere molti dispositivi a un gruppo di risorse contemporaneamente, utilizza la seguente API:

```
 PUT /bulk/devices/{groupId}/add
```

Il gruppo a cui aggiungere i dispositivi deve essere specificato nel percorso della richiesta e i dispositivi da aggiungere devono essere specificati nel corpo della richiesta. Per ulteriori informazioni sullo schema di richiesta e sulle risposte, consulta [{{site.data.keyword.iot_short_notm}} Limited Gateway API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_add){: new_window}.

Per rimuovere più dispositivi da un gruppo di risorse, utilizza la seguente API:

```
PUT /bulk/devices/{groupId}/remove
```

I dispositivi specificati nel corpo della richiesta saranno rimossi dal gruppo specificato nel percorso della richiesta. Per ulteriori informazioni sullo schema della richiesta e sulla risposta, consulta [{{site.data.keyword.iot_short_notm}} Limited Gateway API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_remove){: new_window}.

## Ricerca di un gruppo di risorse
{: #finding_groups}

I gruppi di risorse possono avere associate tag di ricerca. La ricerca delle tag può essere utilizzata per richiamare i dettagli di un gruppo di risorse utilizzando la seguente API:

```
GET /groups
```

Questa API restituisce i gruppi di risorse associati alla tag di ricerca utilizzata. Se non viene specificata alcuna tag di ricerca, vengono restituiti tutti i gruppi di risorse. <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

L'ID di un gruppo di risorse assegnato a un gateway può essere trovato utilizzando la seguente API dove *${clientID}* è il ClientID codificato URL nel formato *d:${orgId}:${typeId}:${deviceId}* per i dispositivi o *g:${orgId}:${typeId}:${deviceId}* per i gateway:

```
GET /authorization/devices/${clientId}
```

Questa API restituisce l'identificativo univoco dei gruppi di risorse assegnati a questo dispositivo. Ulteriori informazioni su questa API possono essere trovate in [{{site.data.keyword.iot_short_notm}} Limited Gateway API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_authorization_devices_deviceId){: new_window}.


## Query di un gruppo di risorse
{: #querying_groups}

È possibile eseguire la query dei gruppi di risorse in vari parametri per restituire le proprietà complete di tutti i dispositivi nel gruppo, gli identificativi univoci di tutti i dispositivi nel gruppo o le proprietà del gruppo di risorse.

Per restituire le proprietà complete di tutti i dispositivi nel gruppo di risorse specificato, utilizza la seguente API:

```
GET /bulk/devices/{groupId}
```

Questa API restituisce l'elenco delle proprietà complete di tutti i membri del gruppo di risorse specificato. Per ulteriori informazioni sullo schema della richiesta, sulle risposte e su come sfogliare i risultati, consulta [{{site.data.keyword.iot_short_notm}} Limited Gateway API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_bulk_devices_groupId){: new_window}.

Per restituire solo gli identificativi univoci dei membri del gruppo di risorse, utilizza la la seguente API:

```
GET /bulk/devices/{groupId}/ids
```

Questa API restituisce gli identificativi univoci di tutti i dispositivi che sono membri del gruppo di risorse. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per restituire le proprietà del gruppo di risorse, utilizza la seguente API:

```
GET /groups/{groupId}
```

Questa API restituisce le proprietà del gruppo di risorse (nome, descrizione, tag di ricerca e identificativo univoco) specificate nel percorso, ma non restituisce l'elenco dei membri del gruppo di risorse. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Creazione ed eliminazione di un gruppo di risorse.
{: #crt_del_groups}

I gruppi di risorse possono essere creati ed eliminati indipendentemente dalla connessione ai gateway. Per creare un gruppo di risorse, utilizza la seguente API:

```
POST /groups
```

Questa API crea un gruppo di risorse e restituisce i dettagli del gruppo. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per eliminare un gruppo di risorse, utilizza la seguente API:

```
DELETE /groups/{groupId}
```

Questa API elimina il gruppo di risorse specificato. I dispositivi che sono membri del gruppo vengono eliminati dal gruppo, ma i dispositivi stessi non sono altrimenti interessati. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Aggiornamento delle proprietà del gruppo
{: #update_groups}

  - /groups/{groupId}
    - PUT: aggiorna le proprietà del gruppo specificato.

## Richiamo e aggiornamento delle proprietà del dispositivo.
{: #fdevice_group_props}

Esistono diversi modi per richiamare le proprietà del dispositivo utilizzando l'API, ogni API restituisce informazioni diverse. Per richiamare le proprietà del dispositivo di tutti i dispositivi esistenti nella tua organizzazione {{site.data.keyword.iot_short_notm}}, utilizza la seguente API:

```
GET /authorization/devices

```

Questa API restituisce le proprietà di tutti i dispositivi esistenti nell'organizzazione, incluse le loro proprietà rilevanti per il controllo dell'accesso (ruolo, stato, data di scadenza). <!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per richiamare le proprietà del dispositivo di un solo dispositivo nell'organizzazione, utilizza la seguente API dove *${clientID}* è il ClientID codificato URL nel formato *d:${orgId}:${typeId}:${deviceId}* per i dispositivi o *g:${orgId}:${typeId}:${deviceId}* per i gateway:

```
GET /authorization/devices/${clientId}
```

Questa API restituisce tutte le proprietà del dispositivo specificato. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

Per richiamare solo le informazioni sul controllo dell'accesso di un dispositivo specifico, utilizza la seguente API dove *${clientID}* è il ClientID codificato URL nel formato *d:${orgId}:${typeId}:${deviceId}* per i dispositivi o *g:${orgId}:${typeId}:${deviceId}* per i gateway:

```
GET /authorization/devices/${clientId}/roles
```

Questa API richiama le informazioni rilevanti per il controllo dell'accesso per il dispositivo specificato senza restituire altre proprietà del dispositivo. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Le proprietà del dispositivo possono essere aggiornate in due modi. Le proprietà possono essere aggiornate senza modificare le proprietà del controllo dell'accesso o le proprietà del controllo dell'accesso possono essere modificate direttamente.

Per aggiornare le proprietà del dispositivo senza influenzare le proprietà del controllo dell'accesso, utilizza la seguente API dove *${clientID}* è il ClientID codificato URL nel formato *d:${orgId}:${typeId}:${deviceId}* per i dispositivi o *g:${orgId}:${typeId}:${deviceId}* per i gateway:

```
PUT /authorization/devices/${clientId}
```

Questa API aggiornerà solo le proprietà del dispositivo non associate al controllo dell'accesso. <!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per aggiornare solo le proprietà del controllo dell'accesso del dispositivo specificato, utilizza la seguente API dove *${clientID}* è il ClientID codificato URL nel formato *d:${orgId}:${typeId}:${deviceId}* per i dispositivi o *g:${orgId}:${typeId}:${deviceId}* per i gateway:

```
PUT /authorization/devices/${clientId}/withroles
```

Questa API aggiornerà solo le proprietà del controllo dell'accesso del dispositivo specificato. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
