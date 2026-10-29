# Chapter 12: How to Extend the Project (Engineering Recipes)

## 1. Recipe: Adding a New Backend API Endpoint

1. **Define Request/Response Schemas**:
   Create or edit schemas in [`app/schemas/`](../../tourvaa-admin-backend/app/schemas):
   ```python
   from pydantic import BaseModel

   class FeatureCreateRequest(BaseModel):
       title: str
       is_active: bool = True
   ```
2. **Implement Business Logic in Service**:
   Add function in [`app/services/`](../../tourvaa-admin-backend/app/services):
   ```python
   def create_feature(db: Session, data: FeatureCreateRequest, actor: User) -> dict:
       feature = Feature(title=data.title, is_active=data.is_active, created_by=actor.id)
       db.add(feature)
       db.commit()
       db.refresh(feature)
       return serialize_feature(feature)
   ```
3. **Mount Route Handler in Router**:
   Add endpoint in [`app/routers/`](../../tourvaa-admin-backend/app/routers):
   ```python
   @router.post("/features")
   def add_feature(
       data: FeatureCreateRequest,
       db: Session = Depends(get_db),
       current_user: User = Depends(require_any_permission("features.create")),
   ):
       return {"status": "success", "data": create_feature(db, data, current_user)}
   ```
4. **Write Test Suite**:
   Create `tests/test_feature.py` asserting status code and database record creation.

---

## 2. Recipe: Adding a New Frontend Page

1. Create directory in [`src/app/`](../../tourvaa-admin-frontend/src/app):
   - Example: `src/app/admin/features/page.tsx`
2. Implement Page Component with Route Protection:
   ```tsx
   "use client";
   import { useQuery } from "@tanstack/react-query";
   import api from "@/lib/api/client";
   import Loader from "@/components/common/Loader";

   export default function FeaturesPage() {
     const { data, isLoading } = useQuery({
       queryKey: ["features"],
       queryFn: async () => (await api.get("/features")).data.data,
     });

     if (isLoading) return <Loader label="Loading features..." />;
     return <div className="p-6"><h1 className="text-xl font-bold">Features</h1></div>;
   }
   ```
