# MyWebAp

// GET: Customer/Create
    public ActionResult Create()
    {
        return View();
    }

    // POST: Customer/Create
    [HttpPost]
    public ActionResult Create(Customer customer)
    {
        try
        {
            // TODO: Add insert logic here
            using (DbModels dbmodel = new DbModels())
            {
                dbmodel.Customers.Add(customer);
                dbmodel.SaveChanges();
            }

                return RedirectToAction("Index");
        }
        catch
        {
            return View();
        }
    }

    // GET: Customer/Edit/5
    public ActionResult Edit(int id)
    {
        using (DbModels dbmodel = new DbModels())
        {
            return View(dbmodel.Customers.Where(x => x.Id == id).FirstOrDefault());
        }
    }

    // POST: Customer/Edit/5
    [HttpPost]
    public ActionResult Edit(int id, Customer customer)
    {
        try
        {
            using (DbModels dbmodel = new DbModels())
            {
                dbmodel.Entry(customer).State = EntityState.Modified;
                dbmodel.SaveChanges();
            }
                // TODO: Add update logic here

                return RedirectToAction("Index");
        }
        catch
        {
            return View();
        }
    }

    // GET: Customer/Delete/5
    public ActionResult Delete(int id)
    {
        using (DbModels dbmodel = new DbModels())
        {
            return View(dbmodel.Customers.Where(x => x.Id == id).FirstOrDefault());
        }
    }

    // POST: Customer/Delete/5
    [HttpPost]
    public ActionResult Delete(int id, FormCollection collection)
    {
        try
        {
            // TODO: Add delete logic here
            using(DbModels dbModel=new DbModels())
            {
                Customer customer = dbModel.Customers.Where(x => x.Id == id).FirstOrDefault();
                dbModel.Customers.Remove(customer);
                dbModel.SaveChanges();
            }
            return RedirectToAction("Index");
        }
        catch
        {
            return View();
        }
    }
}
