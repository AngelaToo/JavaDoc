```java
storeEntityMap = store_list.stream().map(v -> gson.fromJson(v, StoreEntity.class))        .collect(Collectors.groupingBy(StoreEntity::getSp_id));
```

