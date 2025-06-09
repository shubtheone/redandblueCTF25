# Ghost payload - rev

After analysing the file i created a python script to extract resource data from a Windows executable file (GhostPayload.exe) using the pefile.<br>
<br>




```
import pefile
pe = pefile.PE('GhostPayload.exe')
pe.parse_data_directories(directories=[pefile.DIRECTORY_ENTRY['IMAGE_DIRECTORY_ENTRY_RESOURCE']])
for res in pe.DIRECTORY_ENTRY_RESOURCE.entries:
    # Dump each resource entry to a file for inspection
    for sub in res.directory.entries:
        data_rva = sub.directory.entries[0].data.struct.OffsetToData
        size = sub.directory.entries[0].data.struct.Size
        data = pe.get_memory_mapped_image()[data_rva:data_rva+size]
        with open(f'resource_{res.name or res.id}_{sub.id}.bin', 'wb') as out:
            out.write(data)

```
<br>

![image](https://github.com/user-attachments/assets/7ea06ce6-8770-4985-b9e9-6d28ddd90dc3)
